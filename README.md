# VRPTW Search Trajectories Dataset for Reinforcement Learning

## Overview

This dataset contains search trajectories from solving Vehicle Routing Problem with Time Windows (VRPTW) instances using a Large Neighborhood Search (LNS) metaheuristic. The data captures the complete search process, including state transitions, operator selections, and solution quality metrics at each iteration, making it suitable for training reinforcement learning agents to learn effective search strategies.

## Dataset Statistics

- **Total trajectories**: 12,617 search steps
- **Unique VRPTW instances**: 51
- **File format**: CSV (Comma-Separated Values)
- **File size**: ~2.5 MB
- **Encoding**: UTF-8

## File Structure

The dataset is stored in a single CSV file: `merged_experiment_data.csv`

## Column Descriptions

| Column Name | Type | Description |
|------------|------|-------------|
| `instance_name` | string | Identifier of the VRPTW problem instance (e.g., "C1_2_1", "C1_6_1", "C1_10_1") |
| `iteration` | integer | Search iteration number within the trajectory (0-indexed) |
| `current_cost` | float | Total cost of the current solution (distance + penalties) |
| `best_cost` | float | Best cost found so far in the search trajectory |
| `num_routes` | integer | Number of vehicle routes in the current solution |
| `total_demand` | integer | Total customer demand across all routes |
| `avg_route_len` | float | Average number of customers per route |
| `feasibility_penalty` | float | Penalty for constraint violations (time windows, capacity) |
| `perc_unserved_nodes` | float | Percentage of unserved customers (typically 0.0 for feasible solutions) |
| `destroy_op_name` | string | Name of the destroy operator used (e.g., "_destroy_random", "_destroy_worst", "_destroy_cluster") |
| `repair_op_name` | string | Name of the repair operator used (e.g., "_repair_best_insertion", "_repair_regret2") |
| `destroy_op_idx` | integer | Index of the destroy operator in the operator set |
| `repair_op_idx` | integer | Index of the repair operator in the operator set |
| `ruin_frac` | float | Fraction of solution destroyed (between 0.0 and 1.0) |
| `cost_delta` | float | Change in cost from previous iteration (negative = improvement) |
| `is_improvement` | integer | Binary flag: 1 if current iteration improved the solution, 0 otherwise |
| `is_new_best` | integer | Binary flag: 1 if current iteration found a new best solution, 0 otherwise |

## Data Characteristics

### Destroy Operators
- `_destroy_random`: Randomly removes customers from routes
- `_destroy_worst`: Removes customers with worst cost contributions
- `_destroy_cluster`: Removes spatially clustered customers

### Repair Operators
- `_repair_best_insertion`: Greedy best insertion heuristic
- `_repair_regret2`: Regret-2 insertion heuristic

### Instance Types
The dataset includes instances from different problem sizes:
- Small instances (C1_2_*): ~20 routes
- Medium instances (C1_6_*): ~60 routes  
- Large instances (C1_10_*): ~100 routes

## Usage for Reinforcement Learning

### State Representation
The following columns can be used as state features:
- Solution quality: `current_cost`, `best_cost`, `cost_delta`
- Solution structure: `num_routes`, `total_demand`, `avg_route_len`
- Constraint violations: `feasibility_penalty`, `perc_unserved_nodes`
- Search context: `iteration`, `ruin_frac`

### Action Space
The action space consists of operator pairs:
- Destroy operator selection: `destroy_op_idx` (0-2)
- Repair operator selection: `repair_op_idx` (0-1)
- Destruction intensity: `ruin_frac` (continuous or discretized)

### Reward Signal
Potential reward signals:
- `cost_delta`: Immediate cost change (negative = good)
- `is_improvement`: Binary improvement indicator
- `is_new_best`: Binary best solution indicator
- Normalized improvement: `(previous_cost - current_cost) / previous_cost`

### Trajectory Structure
Each trajectory corresponds to solving one VRPTW instance. Trajectories can be grouped by `instance_name` and ordered by `iteration` to reconstruct the complete search process.

## Citation

If you use this dataset in your research, please cite appropriately and acknowledge the source.

## License

Dataset License: CC BY-SA 4.0
This dataset is provided under the terms of the Creative Commons Attribution-ShareAlike 4.0 International License (CC BY-SA 4.0).

Author Attribution
When using or citing this dataset, please credit the author:

Author: Serhii Ostrovetskyi

ORCID: https://orcid.org/0009-0005-4429-6071

Context: This dataset was developed as part of research on Adaptive Large Neighborhood Search (ALNS) for Vehicle Routing Problems with Time Windows (VRPTW).

Terms of Use
Attribution: You must give appropriate credit, provide a link to the license, and indicate if changes were made.

ShareAlike: If you remix, transform, or build upon the material, you must distribute your contributions under the same license as the original.

Disclaimer of Warranties ("AS IS")
THE LICENSED MATERIAL IS PROVIDED BY THE LICENSOR ON AN "AS-IS" AND "AS-AVAILABLE" BASIS. THE LICENSOR MAKES NO REPRESENTATIONS OR WARRANTIES OF ANY KIND CONCERNING THE LICENSED MATERIAL, WHETHER EXPRESS, IMPLIED, STATUTORY, OR OTHER. THIS INCLUDES, WITHOUT LIMITATION, WARRANTIES OF TITLE, MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, NON-INFRINGEMENT, ABSENCE OF LATENT OR OTHER DEFECTS, ACCURACY, OR THE PRESENCE OR ABSENCE OF ERRORS, WHETHER OR NOT KNOWN OR DISCOVERABLE.

TO THE EXTENT POSSIBLE, IN NO EVENT WILL THE LICENSOR BE LIABLE TO YOU ON ANY LEGAL THEORY (INCLUDING, WITHOUT LIMITATION, NEGLIGENCE) OR OTHERWISE FOR ANY DIRECT, SPECIAL, INDIRECT, INCIDENTAL, CONSEQUENTIAL, PUNITIVE, EXEMPLARY, OR OTHER LOSSES, COSTS, EXPENSES, OR DAMAGES ARISING OUT OF THIS LICENSE OR USE OF THE LICENSED MATERIAL.

Recommended Citation Format
If you use this dataset in your research, please cite it as follows:

Serhii Ostrovetskyi, "VRPTW Search Trajectories Dataset for Reinforcement Learning" 2026. ORCID: 0009-0005-4429-6071. Licensed under CC BY-SA 4.0.

## Contact

sergeu.ostrovetskiu.2001@gmail.com
