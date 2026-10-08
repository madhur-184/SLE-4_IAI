# 8-Puzzle Solver and Profiler

## Overview

This project is an 8-Puzzle Solver and Profiler developed as part of SLE-4 for the course 02AML204 – Introduction to Artificial Intelligence.

The system takes a scrambled 3×3 puzzle and finds a sequence of blank-tile moves that reaches the goal state.

The project compares two uninformed search algorithms:

* Breadth-First Search (BFS)
* Depth-Limited Depth-First Search (DFS)

Based on the performance and solution-quality results, BFS was selected as the main solver and DFS was retained as a comparison baseline.

## Student Information

Name: Madhur Pravin Bhandari

PRN: 25UAM116

Course: 02AML204 – Introduction to Artificial Intelligence

GitHub Repository: https://github.com/madhur-184/SLE-4_IAI

## Problem Statement

The 8-Puzzle consists of eight numbered tiles and one blank space arranged on a 3×3 board.

The objective is to move the blank tile until the puzzle reaches the goal state.

The solver searches through possible puzzle states and finds a path from the initial state to the goal state.

## Algorithms Used

### Breadth-First Search (BFS)

BFS uses a FIFO queue as the Frontier and an Explored Set to avoid repeated states.

BFS was selected as the main solver because it returns the shortest solution path for the 8-Puzzle.

### Depth-Limited DFS

Depth-Limited DFS uses a stack as the Frontier with a depth limit of 30.

DFS is included as a comparison baseline. It uses less memory but does not guarantee the shortest solution.

## Architecture

Both BFS and DFS use the same Problem Definition container.

The `get_neighbors()` function is shared by both algorithms so that the comparison remains fair.

The main difference between the two algorithms is the Frontier:

BFS → Queue

DFS → Stack

An Explored Set is used to prevent the same state from being expanded repeatedly.

## Performance Results

The algorithms were tested on 4-move, 12-move and 22-move scrambles.

| Test Case        | Algorithm      | Time (ms) | Nodes Expanded | Path Length |
| ---------------- | -------------- | --------- | -------------- | ----------- |
| 4-move scramble  | BFS            | 0.0364    | 24             | 4           |
| 4-move scramble  | DFS (limit 30) | 43.97     | 42,235         | 4           |
| 12-move scramble | BFS            | 1.664     | 1,128          | 12          |
| 12-move scramble | DFS (limit 30) | 35.42     | 34,661         | 30          |
| 22-move scramble | BFS            | 53.91     | 31,523         | 18          |
| 22-move scramble | DFS (limit 30) | 13.02     | 13,846         | 30          |

The measurements were based on five runs per case using `time.perf_counter` and a manual node counter.

## Why BFS Was Selected

BFS returned the shortest paths for all three test cases:

* 4 moves
* 12 moves
* 18 moves

DFS returned 30-move paths for two of the three test cases because it reached its depth limit before finding a shorter solution.

For the 22-move puzzle, DFS was faster and expanded fewer nodes. However, it returned a 30-move solution instead of the optimal 18-move solution.

Therefore, BFS was selected because it provides optimal and predictable results for this project.

## Advantages of BFS

* Always returns the shortest solution for this problem.
* Simple to implement and test.
* Results are predictable and easy to verify.
* Works with the existing modular architecture.
* Can later be extended with a heuristic module and A*.

## Limitations

BFS requires increasing memory as the search depth increases.

The 8-Puzzle has 9!/2 = 181,440 reachable states, so BFS remains manageable for this problem.

However, BFS would not scale well to much larger puzzles such as the 15-Puzzle.

## Future Work

The next planned improvement is to add a Heuristic Module and implement A* search.

A* using a Manhattan-distance heuristic could reduce the number of nodes expanded compared with uninformed BFS.

The modular architecture allows this improvement without rewriting the existing problem-definition components.

## SLE Journey

### SLE-1

Built a Simple AL Bot.

### SLE-2

Built an 8-Puzzle solver using BFS and depth-limited DFS.

The algorithms were profiled using py-spy and `time.perf_counter` on 4, 12 and 22-move scrambles.

### SLE-3

Designed the C4 model for the system, splitting the project into containers and zooming into the Search Engine.

The `get_neighbors()` function was kept shared between BFS and DFS to maintain a fair comparison.

### SLE-4

Used the findings from the previous SLEs to make the architecture decision to use BFS as the main solver and keep DFS as the comparison baseline.

A* with a heuristic was identified as the next step for larger puzzles.

## AI Contribution

AI tools were used during the preparation of the SLE-4 documentation.

AI Tool Used: Claude (Anthropic)

AI was used for:

* Drafting the ADR layout from the SLE-4 guideline.
* Summarising the SLE-2 and SLE-3 reports.
* Organising information into ADR sections.
* Formatting the documentation.

The following work was completed by the student:

* Building the BFS/DFS solver.
* Profiling the algorithms.
* Collecting the SLE-2 performance measurements.
* Designing the C4 model.
* Selecting BFS as the main solver.
* Checking that the numbers and component names matched the actual project work.
* Preparing to explain and defend the decision during the viva.

