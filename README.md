# SLE-4_IAI

# SLE-4: Architecture Decision Record (ADR) – 8-Puzzle Solver
---

## About this repository

This repository holds my **SLE-4 submission**: one Architecture Decision Record (ADR) that justifies a key design choice in my 8-Puzzle search project, plus an AI contribution log.

**The decision recorded:** use **Breadth-First Search (BFS) with an Explored Set** as the main solver for the 8-Puzzle, instead of depth-limited DFS (limit 30).

## Repository contents

| File | Description |
| --- | --- |
| `SLE4_25UAM116_Madhur-Bhandari.pdf` | Final SLE-4 submission (ADR, SLE journey summary, AI note) |
| `AI_CONTRIBUTION_LOG.md` | Honest record of how AI was used in this SLE |
| `README.md` | This file |

## ADR at a glance

- **Context:** I needed to pick the main uninformed search strategy for the 8-Puzzle, based on solution quality and cost.
- **Decision:** BFS with a FIFO queue as the Frontier and an Explored Set to avoid repeated states. DFS stays only as a comparison baseline.
- **Alternatives considered:** depth-limited DFS, A* with Manhattan distance, and Iterative-Deepening DFS (IDDFS).

### Evidence from SLE-2 profiling

| Test case | Algorithm | Time (ms) | Nodes expanded | Path length |
| --- | --- | --- | --- | --- |
| 4-move scramble | BFS | 0.0364 | 24 | 4 |
| 4-move scramble | DFS (limit 30) | 43.97 | 42,235 | 4 |
| 12-move scramble | BFS | 1.664 | 1,128 | 12 |
| 12-move scramble | DFS (limit 30) | 35.42 | 34,661 | 30 |
| 22-move scramble | BFS | 53.91 | 31,523 | 18 |
| 22-move scramble | DFS (limit 30) | 13.02 | 13,846 | 30 |

**Key takeaways**

- BFS always returned the shortest path (4, 12 and 18 moves). DFS returned 30-move paths on two of the three puzzles.
- Averaged over the three cases, BFS expanded about 2.8x fewer nodes (10,892 vs 30,247).
- Honest exception: DFS was faster on the 22-move puzzle, but only by luck of neighbour order, and its path was longer.
- BFS memory is manageable here because the 8-Puzzle has only 9!/2 = 181,440 reachable states.

### Trade-offs

- Memory grows as O(b^d), so BFS would not scale to a 15-puzzle (about 10^13 states).
- Next step for larger puzzles: add a Heuristic Module (a 7th container in the C4 model) and move to A* / IDA*.

## Connection to my other SLEs

| SLE | Work | Link |
| --- | --- | --- |
| SLE-1 | Simple AI bot | – |
| SLE-2 | BFS vs DFS profiling on the 8-Puzzle (py-spy, `time.perf_counter`) | https://github.com/madhur-184/IAI-SLE |
| SLE-3 | Full C4 architecture model (6 containers, Search Engine components) | https://github.com/madhur-184/SLE-3_IAI |
| SLE-4 | ADR + viva (this repo) | https://github.com/madhur-184/SLE-4_IAI |
