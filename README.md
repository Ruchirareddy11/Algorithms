# AI / PFA Assignment 2
## Search Algorithms, Heuristics and UGV Path Planning

This repository contains **Assignment 2** for the **Artificial Intelligence / Problem Formulation and Analysis (AI/PFA)** course.

The assignment combines theoretical concepts of Artificial Intelligence search algorithms with practical implementations using Python.

The assignment is implemented in a **single Google Colab / Jupyter Notebook**, containing both **Part A – Theory** and **Part B – Programming**.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Objectives](#objectives)
- [Repository Structure](#repository-structure)
- [Part A - Theory](#part-a---theory)
  - [Uninformed Search](#1-uninformed-search)
  - [Informed Search](#2-informed-search)
  - [Heuristics](#3-heuristics)
- [Part B - Programming](#part-b---programming)
  - [Assignment 1 - Dijkstra](#4-dijkstra-algorithm---indian-cities)
  - [Assignment 2 - Static UGV](#5-ugv-path-planning---static-obstacles)
  - [Assignment 3 - Dynamic UGV](#6-ugv-path-planning---dynamic-obstacles)
- [Algorithms Used](#algorithms-used)
- [Technologies Used](#technologies-used)
- [Methodology](#methodology)
- [Performance Measures](#performance-measures)
- [How to Run](#how-to-run)
- [Expected Output](#expected-output)
- [Complexity Analysis](#complexity-analysis)
- [Static vs Dynamic UGV](#static-vs-dynamic-ugv)
- [Learning Outcomes](#learning-outcomes)
- [Future Improvements](#future-improvements)
- [Conclusion](#conclusion)
- [Author](#author)

---

# Project Overview

Search algorithms are fundamental techniques in Artificial Intelligence used to find solutions to problems by exploring a state space.

This assignment focuses on understanding how different search algorithms work and how they can be applied to practical path-finding and autonomous navigation problems.

The assignment is divided into two main sections:

### Part A – Theory

The theoretical section covers:

- Uninformed Search Algorithms
- Informed Search Algorithms
- Heuristic Functions
- Completeness
- Optimality
- Time Complexity
- Space Complexity
- Applications of Search Algorithms

### Part B – Programming

The practical section contains three implementations:

1. **Dijkstra's Algorithm for Indian Cities**
2. **A* UGV Path Planning with Static Obstacles**
3. **A* UGV Path Planning with Dynamic / Unknown Obstacles**

---

# Objectives

The main objectives of this assignment are:

- To understand different search strategies used in Artificial Intelligence.
- To compare uninformed and informed search algorithms.
- To understand the purpose of heuristic functions.
- To understand admissible heuristics.
- To implement Dijkstra's shortest-path algorithm.
- To implement A* search.
- To solve shortest-path problems using weighted graphs.
- To implement grid-based path planning.
- To simulate UGV navigation.
- To handle static obstacles.
- To handle dynamically discovered obstacles.
- To implement dynamic replanning.
- To measure algorithm performance.
- To visualize path-planning results.

---

# Repository Structure

```text
AI-PFA-Assignment-2/
│
├── README.md
│
└── AI_PFA_Assignment_2.ipynb
```

### README.md

This file contains the complete documentation of the assignment.

### AI_PFA_Assignment_2.ipynb

The main Google Colab / Jupyter Notebook containing:

- Part A – Theory
- Part B – Programming
- Python implementations
- Experimental results
- Performance measurements
- Graphs
- Path visualizations

---

# Part A - Theory

# 1. Uninformed Search

Uninformed search algorithms do not use additional information about how close a state is to the goal.

They use only the information available from the problem definition.

The following uninformed search algorithms are studied:

- Breadth-First Search (BFS)
- Uniform-Cost Search (UCS)
- Depth-First Search (DFS)
- Depth-Limited Search (DLS)
- Iterative Deepening Search (IDS)
- Bidirectional Search

---

## 1.1 Breadth-First Search (BFS)

Breadth-First Search explores nodes level by level.

It first explores all nodes at depth 1, then depth 2, then depth 3, and so on.

### Characteristics

- Complete under standard finite-branching assumptions.
- Optimal when all step costs are equal.
- Uses a FIFO queue.
- Can require significant memory.

### Complexity

```text
Time  : O(b^d)
Space : O(b^d)
```

Where:

- `b` = branching factor
- `d` = depth of the shallowest solution

---

## 1.2 Uniform-Cost Search (UCS)

Uniform-Cost Search expands the node with the smallest path cost.

It is useful when actions have different costs.

The evaluation function is:

```text
f(n) = g(n)
```

Where:

- `g(n)` = cost from the starting state to node `n`

### Characteristics

- Complete under standard positive-cost assumptions.
- Optimal for non-negative path costs.
- Uses a priority queue.

Dijkstra's algorithm is closely related to Uniform-Cost Search for shortest-path problems.

---

## 1.3 Depth-First Search (DFS)

Depth-First Search explores one branch as deeply as possible before backtracking.

It can be implemented using:

- Stack
- Recursion

### Advantages

- Low memory requirement.
- Simple implementation.

### Disadvantages

- Can explore very deep paths.
- Not generally optimal.
- May not be complete in infinite-depth spaces.

### Complexity

```text
Time  : O(b^m)
Space : O(bm)
```

Where:

- `b` = branching factor
- `m` = maximum search depth

---

## 1.4 Depth-Limited Search (DLS)

Depth-Limited Search is a modified version of DFS with a predefined depth limit.

For example:

```text
Depth Limit = 5
```

The search does not explore nodes beyond depth 5.

This prevents DFS from searching indefinitely deep.

---

## 1.5 Iterative Deepening Search (IDS)

Iterative Deepening Search repeatedly performs depth-limited searches with increasing depth limits.

For example:

```text
Depth Limit = 0
Depth Limit = 1
Depth Limit = 2
Depth Limit = 3
...
```

until the goal is found.

IDS combines:

- The memory efficiency of DFS.
- The completeness of BFS under standard assumptions.
- Optimality for equal step costs.

---

## 1.6 Bidirectional Search

Bidirectional Search performs two searches:

```text
Start → Goal
```

and:

```text
Goal → Start
```

The searches continue until they meet.

For suitable problems, the search depth can be approximately reduced from:

```text
O(b^d)
```

to:

```text
O(b^(d/2))
```

The method requires that the problem supports an appropriate reverse search.

---

# 2. Informed Search

Informed search algorithms use additional knowledge about the problem to guide the search.

This additional information is generally provided through a heuristic function.

The following informed search algorithms are studied:

- Greedy Best-First Search
- Best-First Search
- Dijkstra's Algorithm
- A* Search
- Beam Search
- Recursive Best-First Search (RBFS)
- Iterative Deepening A* (IDA*)
- Weighted A*

---

## 2.1 Greedy Best-First Search

Greedy Best-First Search selects the node that appears closest to the goal according to the heuristic.

The evaluation function is:

```text
f(n) = h(n)
```

Where:

- `h(n)` = estimated cost from node `n` to the goal.

It can reduce search effort but is not generally optimal.

---

## 2.2 Best-First Search

Best-First Search selects the most promising node according to an evaluation function.

A priority queue is normally used to select the next node.

Different evaluation functions result in different versions of best-first search.

---

## 2.3 Dijkstra's Algorithm

Dijkstra's algorithm finds the shortest path in a graph containing non-negative edge weights.

Its evaluation function can be represented as:

```text
f(n) = g(n)
```

Where:

- `g(n)` = actual cost from the start node to `n`.

Dijkstra's algorithm is implemented in this assignment for finding routes between Indian cities.

---

## 2.4 A* Search

A* combines the actual cost travelled with an estimated remaining cost.

The evaluation function is:

```text
f(n) = g(n) + h(n)
```

Where:

- `g(n)` = actual cost from start to current node.
- `h(n)` = estimated cost from current node to goal.
- `f(n)` = estimated total path cost through node `n`.

A* is used in both UGV path-planning implementations.

---

## 2.5 Beam Search

Beam Search is a memory-limited search strategy.

Instead of retaining all candidate nodes, it keeps only a fixed number of the most promising nodes.

This number is called the:

```text
Beam Width
```

A smaller beam width reduces memory usage but can discard paths that might lead to better solutions.

---

## 2.6 Recursive Best-First Search (RBFS)

Recursive Best-First Search is a memory-efficient informed search algorithm.

RBFS attempts to achieve behavior similar to best-first search while using substantially less memory.

It recursively explores the most promising path while maintaining an alternative path cost.

---

## 2.7 Iterative Deepening A* (IDA*)

IDA* combines iterative deepening with the A* evaluation function:

```text
f(n) = g(n) + h(n)
```

Instead of storing a large priority queue, the algorithm repeatedly searches using increasing `f`-cost thresholds.

This provides a way to reduce memory requirements.

---

## 2.8 Weighted A*

Weighted A* modifies the A* evaluation function:

```text
f(n) = g(n) + w × h(n)
```

Where:

```text
w > 1
```

Increasing the heuristic weight gives more importance to the estimated distance to the goal.

This can reduce search effort, but optimality is generally sacrificed.

---

# 3. Heuristics

A heuristic is an estimate of the cost required to reach a goal from a particular state.

It is represented by:

```text
h(n)
```

A good heuristic can reduce the number of states that need to be explored.

---

## 3.1 Satisficing Search

Satisficing search attempts to find a solution that is good enough rather than necessarily optimal.

The main objective is often:

```text
Find an acceptable solution quickly.
```

This can be useful when computational time is more important than obtaining the mathematically optimal solution.

---

## 3.2 Admissible Heuristic

A heuristic is admissible if it never overestimates the true minimum cost from a state to the goal.

Mathematically:

```text
0 ≤ h(n) ≤ h*(n)
```

Where:

- `h(n)` = estimated cost.
- `h*(n)` = actual optimal remaining cost.

Admissibility is important for optimal A* search under the standard assumptions of the algorithm.

---

## 3.3 Formulating Heuristics

A heuristic can often be created by simplifying the original problem.

For example, in a grid-navigation problem, obstacles can be ignored to calculate a lower-bound distance to the goal.

Common distance-based heuristics include:

- Manhattan Distance
- Euclidean Distance
- Chebyshev Distance
- Octile Distance

---

## 3.4 Heuristics from Subproblems

A heuristic can be created by solving a simpler version of the original problem.

The general process is:

```text
Original Problem
       ↓
Simplified Problem
       ↓
Solve Simplified Problem
       ↓
Use Result as Heuristic
```

If multiple admissible heuristics are available, they can be combined using:

```text
h(n) = max(h1(n), h2(n))
```

When both `h1` and `h2` are admissible, their maximum is also admissible.

---

# Part B - Programming

# 4. Dijkstra Algorithm - Indian Cities

## 4.1 Objective

The first programming task implements Dijkstra's algorithm to find the shortest path between cities connected by roads with different distances.

The problem is represented as a weighted graph.

---

## 4.2 Graph Representation

The graph represents:

```text
Cities       → Nodes / Vertices
Roads        → Edges
Distance     → Edge Weights
Start City   → Source
Goal City    → Destination
```

For example:

```text
Hyderabad ---- 570 km ---- Bengaluru
      |
      |
    625 km
      |
      ↓
   Chennai
```

The graph is stored using an adjacency-list representation.

---

## 4.3 Dijkstra Methodology

The algorithm follows these steps:

```text
1. Set the distance of the source city to 0.
2. Set the distance of all other cities to infinity.
3. Insert the source city into a priority queue.
4. Select the city with the smallest known distance.
5. Examine its neighboring cities.
6. Calculate the new distance.
7. Update the distance if a shorter path is found.
8. Continue until the destination is reached.
9. Reconstruct the shortest path.
```

---

## 4.4 User Input

The program accepts:

```text
Starting City
Goal City
```

City names are handled in a case-insensitive manner.

For example:

```text
hyderabad
Hyderabad
HYDERABAD
```

are interpreted as the same city.

---

## 4.5 Dijkstra Output

The program displays:

- Starting city
- Goal city
- Shortest path
- Total distance
- Number of road segments
- Execution time

Example output format:

```text
======================================
          SHORTEST PATH
======================================

Hyderabad → Mumbai → Pune → Ahmedabad → Delhi

Total Distance : XXX km
Road Segments  : X
Execution Time : X ms
```

---

## 4.6 Dijkstra Complexity

With a binary heap priority queue:

```text
Time Complexity:
O((V + E) log V)
```

Where:

- `V` = number of cities.
- `E` = number of roads.

---

# 5. UGV Path Planning - Static Obstacles

## 5.1 Objective

The second programming task implements A* path planning for an Unmanned Ground Vehicle (UGV) operating in a grid containing static obstacles.

The UGV must find a shortest collision-free route from the start position to the goal position.

---

## 5.2 Environment

The environment is a:

```text
70 × 70
```

grid.

### Start

```text
(0, 0)
```

### Goal

```text
(69, 69)
```

### Obstacle Densities

Three different environments are evaluated:

```text
Low Density       → 15%
Medium Density    → 25%
High Density      → 35%
```

---

## 5.3 Grid Representation

Each cell represents a possible UGV position.

A cell can be:

```text
Free Cell
```

or:

```text
Obstacle Cell
```

The starting and goal cells are always kept free.

---

## 5.4 Movement Model

The UGV can move in eight directions:

```text
        ↑
     ↖  │  ↗
        │
←───────┼───────→
        │
     ↙  │  ↘
        ↓
```

The allowed movements are:

- Up
- Down
- Left
- Right
- Up-Left
- Up-Right
- Down-Left
- Down-Right

---

## 5.5 Movement Cost

Horizontal and vertical movement:

```text
Cost = 1
```

Diagonal movement:

```text
Cost = √2
```

This allows the algorithm to calculate a more realistic path distance.

---

## 5.6 Collision Checking

The UGV cannot enter an obstacle cell.

For diagonal movements, the implementation also checks the two adjacent cells.

This prevents the UGV from moving diagonally through the corner of two obstacles.

---

## 5.7 A* Algorithm

A* is used to find the path.

The evaluation function is:

```text
f(n) = g(n) + h(n)
```

Where:

```text
g(n) = cost from start to current node
h(n) = estimated cost from current node to goal
```

---

## 5.8 Octile Distance Heuristic

Since the UGV can move horizontally, vertically, and diagonally, the Octile Distance heuristic is used.

The formula is:

```text
h(n) = max(dx, dy) + (√2 - 1) × min(dx, dy)
```

Where:

```text
dx = |x1 - x2|
dy = |y1 - y2|
```

This heuristic matches the movement model used by the UGV.

---

## 5.9 Static Environment Experiments

The algorithm is executed for three obstacle densities:

### Low Density

```text
15% obstacles
```

### Medium Density

```text
25% obstacles
```

### High Density

```text
35% obstacles
```

The same random seed is used for reproducibility.

---

## 5.10 Measurements

For every experiment, the following values are recorded:

| Metric | Description |
|---|---|
| Obstacle Density | Percentage of blocked cells |
| Obstacles | Number of obstacle cells |
| Path Found | Whether a valid route exists |
| Path Distance | Total route distance |
| Path Cells | Number of cells in the path |
| Nodes Explored | Number of states expanded |
| Execution Time | Search execution time |

---

## 5.11 Path Visualization

The notebook generates visualizations for each obstacle density.

The visualization shows:

- Obstacles
- Start position
- Goal position
- Calculated UGV path

This provides a visual representation of the search result.

---

## 5.12 Performance Graphs

The notebook generates performance graphs.

### Graph 1: Obstacle Density vs Nodes Explored

This graph shows how the search effort changes as obstacle density increases.

### Graph 2: Obstacle Density vs Execution Time

This graph shows how obstacle density affects the execution time of A*.

---

## 5.13 Static UGV Analysis

Increasing obstacle density reduces the amount of free space available to the UGV.

This can cause:

```text
More constrained movement
        ↓
More difficult path planning
        ↓
Potentially more states explored
        ↓
Potentially higher execution time
```

At sufficiently high obstacle density, a valid path may not exist.

The actual result depends on the generated obstacle configuration.

---

# 6. UGV Path Planning - Dynamic / Unknown Obstacles

## 6.1 Objective

The third programming task extends the UGV path-planning problem to an environment where the complete obstacle map is not known initially.

The UGV must discover obstacles while moving and update its path accordingly.

---

## 6.2 Dynamic Environment

The simulation uses a:

```text
50 × 50
```

grid.

### Starting Position

```text
(0, 0)
```

### Goal Position

```text
(49, 49)
```

The actual obstacle map exists internally, but the UGV initially has no complete knowledge of it.

---

## 6.3 Initial Knowledge

At the beginning:

```text
Known Obstacles = 0
```

The UGV gradually builds its internal map as it moves.

---

## 6.4 Sensor Simulation

A simulated sensor is used to detect obstacles near the current UGV position.

The sensor operates within a radius of:

```text
2 cells
```

When an obstacle is detected, it is added to the UGV's known obstacle map.

---

## 6.5 Dynamic Navigation Process

The navigation process is:

```text
Detect
   ↓
Plan
   ↓
Move
   ↓
Detect New Obstacles
   ↓
Update Map
   ↓
Replan
   ↓
Move
   ↓
Goal Reached?
   ↓
Finish
```

---

## 6.6 Dynamic A*

The UGV uses A* to calculate a path using the obstacles that are currently known.

If new obstacles are discovered, the UGV updates its internal map and calculates a new route.

This allows the UGV to adapt to new information.

---

## 6.7 Dynamic Simulation

The simulation performs the following operations:

```text
1. Start at the initial position.
2. Detect nearby obstacles.
3. Update the known obstacle map.
4. Calculate a path using A*.
5. Move a small number of steps.
6. Detect newly visible obstacles.
7. If necessary, update the map.
8. Recalculate the route.
9. Continue until the goal is reached.
```

---

## 6.8 Dynamic UGV Measures

The following measures are recorded:

| Measure | Description |
|---|---|
| Goal Reached | Whether the destination was reached |
| Steps | Number of movement steps |
| Distance | Total distance travelled |
| Replans | Number of replanning operations |
| Obstacles Discovered | Number of detected obstacles |
| Execution Time | Total execution time |

---

## 6.9 Dynamic Navigation Concept

The static environment follows:

```text
Complete Map
     ↓
Plan
     ↓
Move
     ↓
Goal
```

The dynamic environment follows:

```text
Partial Map
     ↓
Plan
     ↓
Move
     ↓
Sense
     ↓
Update Map
     ↓
Replan
     ↓
Move
     ↓
Goal
```

This demonstrates the concept of online path planning in a partially known environment.

---

# Algorithms Used

| Algorithm | Category | Application |
|---|---|---|
| BFS | Uninformed Search | Theory |
| UCS | Uninformed Search | Theory |
| DFS | Uninformed Search | Theory |
| DLS | Uninformed Search | Theory |
| IDS | Uninformed Search | Theory |
| Bidirectional Search | Uninformed Search | Theory |
| Greedy Best-First | Informed Search | Theory |
| Best-First Search | Informed Search | Theory |
| Dijkstra | Cost-Based Search | Indian Cities |
| A* | Informed Search | Static UGV |
| Beam Search | Informed Search | Theory |
| RBFS | Informed Search | Theory |
| IDA* | Informed Search | Theory |
| Weighted A* | Informed Search | Theory |

---

# Technologies Used

## Programming Language

```text
Python
```

## Development Environment

```text
Google Colab
Jupyter Notebook
```

## Libraries

### Python `heapq`

Used to implement priority queues for Dijkstra and A*.

```python
import heapq
```

### Pandas

Used to organize experimental results into tables.

```python
import pandas as pd
```

### Matplotlib

Used for path visualizations and performance graphs.

```python
import matplotlib.pyplot as plt
```

### Random

Used to generate obstacle environments.

```python
import random
```

### Math

Used for distance calculations and heuristic functions.

```python
import math
```

### Time

Used to measure algorithm execution time.

```python
import time
```

---

# Methodology

The overall methodology of the project can be summarized as:

```text
                    AI SEARCH
                       │
          ┌────────────┴────────────┐
          │                         │
      THEORY                    PRACTICAL
          │                         │
  ┌───────┴───────┐        ┌───────┼────────┐
  │               │        │       │        │
Uninformed     Informed  Dijkstra  A*     Dynamic A*
 Search         Search     │       │        │
  │               │        │       │        │
BFS             Greedy   Cities  Static   Dynamic
UCS             A*               UGV      UGV
DFS             RBFS
DLS             IDA*
IDS             Beam
Bidirectional   Weighted A*
```

---

# Performance Measures

The assignment evaluates the algorithms using several performance metrics.

## 1. Path Distance

Represents the total cost of the generated route.

For the UGV:

```text
Straight Movement = 1
Diagonal Movement = √2
```

---

## 2. Nodes Explored

Represents the number of states expanded by the search algorithm.

It provides an indication of the search effort.

---

## 3. Execution Time

The execution time is measured using Python's high-resolution timer.

The measurement is reported in milliseconds.

---

## 4. Path Cells

Represents the number of cells contained in the generated UGV route.

---

## 5. Replanning Operations

For dynamic navigation, the number of times the UGV recalculates its path is recorded.

---

## 6. Obstacles Discovered

For the dynamic environment, the number of previously unknown obstacles detected by the UGV is recorded.

---

# Complexity Analysis

## Breadth-First Search

```text
Time  : O(b^d)
Space : O(b^d)
```

---

## Depth-First Search

```text
Time  : O(b^m)
Space : O(bm)
```

---

## Dijkstra

Using a binary heap:

```text
O((V + E) log V)
```

---

## A*

The worst-case time and space complexity can be exponential in solution depth, depending on the search space and heuristic.

In practice, the effectiveness of A* strongly depends on the quality of the heuristic.

A more informative heuristic can reduce the number of states explored.

---

# Static vs Dynamic UGV

| Feature | Static UGV | Dynamic UGV |
|---|---|---|
| Environment | Known | Partially Unknown |
| Obstacles | Static | Discovered during movement |
| Initial Map | Complete | Incomplete |
| Algorithm | A* | Repeated A* |
| Replanning | Generally not required | Required |
| Sensor | Not required | Simulated |
| Path Adaptation | Limited | Dynamic |
| Main Challenge | Collision-free shortest path | Adaptation to new information |

---

# Dijkstra vs A*

| Feature | Dijkstra | A* |
|---|---|---|
| Search Type | Cost-based | Informed |
| Heuristic | No | Yes |
| Evaluation | `g(n)` | `g(n) + h(n)` |
| Main Application | City route planning | UGV navigation |
| Guidance Toward Goal | No heuristic guidance | Uses heuristic |
| Shortest Path | Yes for non-negative edge weights | Yes under standard conditions with an appropriate heuristic |
| Search Efficiency | Can explore many unnecessary nodes | Can reduce exploration with a useful heuristic |

---

# Reproducibility

Random obstacle generation uses fixed random seeds.

For example:

```python
seed = 42
```

This allows the same obstacle configuration to be generated when the notebook is executed again under the same conditions.

The dynamic environment also uses a fixed seed.

This makes it easier to reproduce and compare experimental results.

---

# How to Run

## Option 1 – Google Colab

Google Colab is the recommended environment.

### Step 1

Open Google Colab:

https://colab.research.google.com/

### Step 2

Upload:

```text
AI_PFA_Assignment_2.ipynb
```

### Step 3

Run the notebook cells sequentially from top to bottom.

No external dataset or special hardware is required for the implemented demonstrations.

---

## Option 2 – Jupyter Notebook

Install Python and Jupyter Notebook.

Run:

```bash
jupyter notebook
```

Then open:

```text
AI_PFA_Assignment_2.ipynb
```

Execute the cells sequentially.

---

# Expected Output

## Dijkstra

The notebook displays:

```text
======================================
       INDIAN CITIES SHORTEST PATH
          DIJKSTRA ALGORITHM
======================================

Available Cities:
...

Enter starting city:
Enter goal city:

Shortest Path:
City → City → City

Total Distance : XXX km
Road Segments  : X
Execution Time : X ms
```

---

## Static UGV

The notebook produces a result table containing:

```text
Density
Obstacle %
Obstacles
Path Found
Path Distance
Path Cells
Nodes Explored
Execution Time
```

It also produces visualizations for:

```text
15% Obstacle Density
25% Obstacle Density
35% Obstacle Density
```

and performance graphs for:

```text
Obstacle Density vs Nodes Explored
Obstacle Density vs Execution Time
```

---

## Dynamic UGV

The notebook displays:

```text
======================================
       DYNAMIC UGV SIMULATION
======================================

Goal Reached
Final Position
Steps
Distance Travelled
Replanning Operations
Obstacles Discovered
Execution Time
```

---

# Notebook Organization

The complete notebook follows the structure:

```text
AI / PFA ASSIGNMENT 2
│
├── PART A – THEORY
│   │
│   ├── 1. Uninformed Search
│   ├── 2. Informed Search
│   └── 3. Heuristics
│
└── PART B – PROGRAMMING
    │
    ├── 4. Dijkstra – Indian Cities
    │   ├── Graph Creation
    │   ├── Dijkstra Implementation
    │   ├── User Input
    │   ├── Shortest Path
    │   └── Performance Measurement
    │
    ├── 5. Static UGV
    │   ├── Grid Creation
    │   ├── Obstacle Generation
    │   ├── Movement Model
    │   ├── Octile Heuristic
    │   ├── A* Implementation
    │   ├── 15% Density
    │   ├── 25% Density
    │   ├── 35% Density
    │   ├── Visualization
    │   └── Performance Graphs
    │
    └── 6. Dynamic UGV
        ├── Unknown Environment
        ├── Hidden Obstacles
        ├── Sensor Simulation
        ├── Known Obstacle Map
        ├── A* Planning
        ├── Dynamic Detection
        ├── Replanning
        └── Performance Results
```

---

# Key Concepts Demonstrated

## State

A state represents a possible situation in the problem.

Examples:

```text
City → Hyderabad
Grid Cell → (20, 35)
```

---

## Initial State

The state from which the search starts.

Examples:

```text
City Route:
Hyderabad
```

```text
UGV:
(0, 0)
```

---

## Goal State

The desired final state.

Examples:

```text
City Route:
Delhi
```

```text
UGV:
(69, 69)
```

---

## Action

An operation that moves the search from one state to another.

For the UGV, actions include:

```text
Move Up
Move Down
Move Left
Move Right
Move Diagonally
```

---

## Path Cost

The total cost accumulated while moving from the start state to a particular state.

For the UGV:

```text
Horizontal / Vertical = 1
Diagonal              = √2
```

---

## Heuristic

An estimated cost from the current state to the goal.

For the UGV:

```text
Octile Distance
```

is used.

---

# Applications

The concepts implemented in this assignment can be applied to real-world problems such as:

### Navigation

Finding routes between geographical locations.

### Robotics

Planning collision-free movement for autonomous robots.

### Autonomous Vehicles

Finding safe routes in road and grid environments.

### Games

Finding paths for game characters.

### Logistics

Finding efficient routes for transportation.

### Warehouse Robots

Navigating robots around obstacles.

### Military and Defense Robotics

Planning routes for unmanned ground vehicles.

### Search and Rescue

Finding paths through complex environments.

---

# Future Improvements

The current implementation can be extended in several ways.

## 1. Larger Indian City Dataset

The city graph can be expanded with more Indian cities and a larger road network.

---

## 2. Real Road Network

Real-world geographical road data can be incorporated instead of manually defined road connections.

---

## 3. Interactive UGV Environment

The UGV simulation could be converted into an interactive application where users can:

- Place obstacles.
- Select start and goal.
- Change obstacle density.
- Run A*.
- Visualize the search process.

---

## 4. Real-Time Dynamic Obstacles

The dynamic environment could be extended to include obstacles that actually move over time.

---

## 5. Advanced Path Planning

Other algorithms could be compared, including:

- D* 
- D* Lite
- Lifelong Planning A*
- RRT
- RRT*
- Bidirectional A*

---

## 6. Robotics Simulation

The UGV could be implemented in a robotics simulation environment such as:

- ROS
- Gazebo
- Webots
- PyBullet

---

## 7. Sensor Noise

The sensor model could be improved by introducing:

- False positives
- False negatives
- Limited sensing angles
- Sensor range limitations
- Measurement noise

---

# Learning Outcomes

After completing this assignment, the following concepts and skills are demonstrated:

- Understanding Artificial Intelligence search algorithms.
- Understanding uninformed search.
- Understanding informed search.
- Understanding heuristic functions.
- Understanding admissibility.
- Understanding completeness.
- Understanding optimality.
- Understanding search complexity.
- Implementing Dijkstra's algorithm.
- Implementing A* search.
- Working with weighted graphs.
- Working with grid environments.
- Generating obstacle maps.
- Performing collision-free path planning.
- Measuring algorithm performance.
- Visualizing search results.
- Handling partially known environments.
- Implementing dynamic replanning.
- Understanding autonomous navigation.

---

# Conclusion

This assignment demonstrates the application of classical Artificial Intelligence search techniques to practical path-planning problems.

The theoretical section introduces different uninformed and informed search algorithms and explains the role of heuristic functions in guiding search.

The first practical implementation applies Dijkstra's algorithm to a weighted graph representing connections between Indian cities. The system calculates the shortest route and reports the total travel distance and execution time.

The second implementation applies A* to a 70 × 70 UGV environment containing static obstacles. Multiple obstacle densities are evaluated, and the resulting paths and performance measurements are visualized.

The third implementation extends the problem to a partially unknown environment. The UGV detects obstacles using a simulated sensor, updates its internal map, and performs replanning when new information is discovered.

The overall progression of the assignment can be represented as:

```text
AI Search Theory
       ↓
Uninformed Search
       ↓
Informed Search
       ↓
Heuristic Search
       ↓
Dijkstra
       ↓
A* Search
       ↓
Static UGV Navigation
       ↓
Dynamic UGV Navigation
       ↓
Online Replanning
```

The assignment therefore provides a practical understanding of how search algorithms can be used to solve shortest-path, navigation, and autonomous-robot planning problems.

---

# Author

**Ruchira**

**M.Tech**

---

# Project Information

| Information | Details |
|---|---|
| Course | Artificial Intelligence / Problem Formulation and Analysis |
| Assignment | Assignment 2 |
| Language | Python |
| Environment | Google Colab / Jupyter Notebook |
| Search Algorithms | Dijkstra, A* and others |
| Main Application | Shortest Path and UGV Navigation |
| Notebook | `AI_PFA_Assignment_2.ipynb` |

---

## ⭐ Assignment Summary

```text
Part A
├── Uninformed Search
├── Informed Search
└── Heuristics

Part B
├── Dijkstra – Indian Cities
├── Static UGV – A*
└── Dynamic UGV – A* + Replanning
```

**Artificial Intelligence / PFA Assignment 2 – Search Algorithms, Heuristics and UGV Path Planning**
