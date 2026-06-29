# 8-Puzzle AI Solver

> An animated, interactive solver for the classic 8-puzzle (3×3 sliding tile) problem, implementing four search algorithms with real-time performance comparison.

---

## Overview

The 8-puzzle consists of a 3×3 grid containing tiles numbered 1–8 and one blank space. The goal is to slide tiles into the goal configuration `[1, 2, 3 / 4, 5, 6 / 7, 8, _]`. This project visualises that solving process using four AI search strategies, animating each step of the solution path and reporting performance metrics side-by-side.

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Python 3 |
| GUI | Tkinter |
| Data Structures | `heapq` (priority queue), `collections.deque` |
| Course | Artificial Intelligence Lab |

---

## Features

- **Four Search Algorithms** — BFS, DFS (depth-limited to 25), Greedy Best-First, and A* all implemented from scratch
- **Animated Solution Playback** — each move is rendered at 500 ms intervals so the solution path is visible step-by-step
- **Performance Metrics Panel** — after every run, the UI displays steps taken, nodes expanded, and wall-clock time
- **Solvability Guarantee** — `random_state()` uses inversion-count parity to ensure only solvable puzzles are generated; it also rejects the already-solved state
- **Manhattan Distance Heuristic** — used by both Greedy and A* to estimate cost to goal; computed per tile against its target position
- **One-Click Randomise** — generate a fresh puzzle instantly without restarting the application

---

## Algorithm Summary

| Algorithm | Strategy | Optimal? | Notes |
|---|---|---|---|
| BFS | Level-by-level exploration | ✅ Yes | Guarantees shortest path; high memory use |
| DFS | Stack-based depth-first | ❌ No | Depth limit of 25 prevents infinite loops |
| Greedy | Priority by `h(n)` only | ❌ No | Fast but may miss shorter solutions |
| A\* | Priority by `g(n) + h(n)` | ✅ Yes | Optimal with admissible heuristic (Manhattan) |

---

## Project Structure

```
8X8_Puzzle_-_AI/
├── Code.py                     # All logic: algorithms, GUI, utilities
└── AI lab Report(Final).docx   # Lab report with analysis and results
```

---

## How to Run

**Prerequisites:** Python 3.x (Tkinter ships with the standard library — no pip installs needed)

```bash
python Code.py
```

1. A random solvable puzzle loads on startup.
2. Click **BFS**, **DFS**, **Greedy**, or **A\*** to solve it with that algorithm.
3. Watch the tile animation; metrics appear below the grid when it finishes.
4. Click **Random Puzzle** to generate a new board and run again.

---

## Key Implementation Details

- **State representation** — the board is a Python `tuple` of 9 integers; immutable, hashable, and safe to use as dictionary keys in the `parent` map.
- **Neighbour generation** — the blank tile's row/column is computed with `divmod(index, 3)`, then all four cardinal directions are checked against board bounds.
- **Path reconstruction** — a `parent` dictionary maps each state to its predecessor; `reconstruct()` traces back from the goal to the start and reverses the list.
- **DFS depth cap** — without a limit, DFS on the 8-puzzle can visit an unbounded number of states. The cap of 25 is a practical safeguard; most solvable puzzles have optimal solutions well under this depth.

---

## Sample Output (Metrics Panel)

```
A*
Steps: 18
Nodes Expanded: 312
Time: 0.0041s
```

---

## Course Context

Submitted as part of the **Artificial Intelligence Lab** course. The accompanying report (`AI lab Report(Final).docx`) documents algorithm comparisons, state-space analysis, and per-algorithm performance tables.
