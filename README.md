# Traveling Salesman Job Processing Problem with 2-Opt Heuristic

## Description
This project addresses the **Traveling Salesman Job Processing Problem (TSJP)**, a combinatorial optimization problem that integrates the classic Traveling Salesman Problem (TSP) with job scheduling constraints. The model finds an optimal tour visiting all nodes and assigns jobs at each location to minimize the makespan (Cmax).

The solution approach combines:
1. **Optimal TSP resolution** using Mixed Integer Linear Programming (MILP)
2. **Job assignment optimization** based on arrival times
3. **2-opt local search heuristic** to improve the overall solution quality

## Problem Formulation

### TSJP Components
- **TSP Component**: Find the optimal tour visiting all nodes starting and ending at depot (node 0)
- **Job Assignment Component**: Assign one job to each node to minimize total completion time
- **Objective**: Minimize the makespan (Cmax) - the maximum completion time across all jobs

### Key Constraints
- Each node must be visited exactly once
- Each job must be assigned to exactly one node
- Jobs can only start after arrival at the corresponding node
- Subtour elimination constraints ensure a single connected tour

## Implementation Details

### Technologies Used
- **Language**: Mosel (Xpress Optimization)
- **Solver**: Xpress Optimizer (FICO Xpress)
- **Optimization Techniques**: 
  - Mixed Integer Linear Programming (MILP)
  - 2-opt local search heuristic

### Algorithm Phases

#### Phase 1: Optimal TSP Resolution
Solves the TSP using MILP with subtour elimination constraints to find the optimal tour and calculate arrival times at each node.

#### Phase 2: Initial Job Assignment
Given the arrival times from Phase 1, solves an assignment problem to minimize the initial makespan.

#### Phase 3: 2-Opt Improvement
Applies a 2-opt local search heuristic to iteratively improve the tour:
- Tests all possible edge swaps
- Recalculates arrival times for each candidate tour
- Uses a greedy heuristic to estimate Cmax improvements
- Accepts improvements and continues until no better solution is found

#### Final Phase: Optimal Assignment
Once the best tour is identified, solves a final assignment problem to determine the optimal job allocation.

## Input Format

The model requires a data file (`istanza.dat`) with the following structure:
```
n: [number_of_nodes]

t: [
  ! Travel time matrix (n+1 x n+1)
  ! t(i,j) = travel time from node i to node j
]

p: [
  ! Processing time matrix (n+1 x n+1)  
  ! p(i,j) = processing time of job j at node i
]
```

## How to Run

### Prerequisites
- FICO Xpress Optimization Suite installed
- Mosel compiler and runtime

### Execution
```bash
mosel TSJP_2opt.mos
```

### Input File
Ensure `istanza.dat` is in the same directory as the model file.

## Output

The model provides comprehensive output including:

### Solution Comparison
- Initial TSP tour cost and Cmax
- Final tour cost and Cmax after 2-opt improvement
- Number of 2-opt iterations performed

### Final Solution Details
- Optimal tour sequence
- Arrival times at each node
- Job assignments with completion times
- Total execution time

### Example Output

=== FINAL RESULTS ===
Total execution time: X.XX seconds
2-opt iterations executed: X

SOLUTION COMPARISON:
Initial solution (optimal TSP):
  TSP tour cost: XXX.XX
  Initial Cmax: XXX.XX

Final solution (after 2-opt):
  TSP tour cost: XXX.XX
  Final Cmax: XXX.XX

Final tour: 0 3 1 4 2 0
Final optimal job assignment:
Node 1 (T=XX.X) -> Job 3 (proc. time=XX.X, end=XX.X)
...
```

## Key Features

 **Exact TSP Solution**: Uses MILP for guaranteed optimal initial tour  
 **Integrated Optimization**: Combines routing and scheduling in a unified framework  
 **Local Search Enhancement**: 2-opt heuristic improves solution quality  
 **Comprehensive Reporting**: Detailed comparison between initial and improved solutions  
 **Flexible Input**: Easy-to-modify data file format


## Author

Gianmarco Calvi  
Bachelor's Thesis in Operations Research  
Politecnico di Torino

## License

This project is available for academic and educational purposes.

---

For questions or suggestions, please contact: calvigianmarco@gmail.com
