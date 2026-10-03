# AI / PFA Assignment 2

## Artificial Intelligence / Problem Formulation and Analysis

This repository contains **Assignment 2** for Artificial Intelligence / Problem Formulation and Analysis (AI/PFA).

The assignment includes both **theoretical concepts** and **practical implementations** of uninformed and informed search algorithms.

---

## 📌 Contents

### Part A – Theory

1. **Uninformed Search Algorithms**
   - Breadth-First Search (BFS)
   - Uniform-Cost Search (UCS)
   - Depth-First Search (DFS)
   - Depth-Limited Search (DLS)
   - Iterative Deepening Search (IDS)
   - Bidirectional Search

2. **Informed Search Algorithms**
   - Greedy Best-First Search
   - Best-First Search
   - Dijkstra's Algorithm
   - A* Search
   - Beam Search
   - Recursive Best-First Search (RBFS)
   - Iterative Deepening A* (IDA*)
   - Weighted A*

3. **Heuristics**
   - Satisficing Search
   - Admissible Heuristics
   - Formulation of Heuristics
   - Heuristics from Subproblems

---

# Part B – Programming

## 1. Dijkstra's Algorithm – Indian Cities

### Objective

Implement Dijkstra's algorithm to find the shortest path between cities in India using a weighted graph.

### Representation

- Cities → Nodes
- Roads → Edges
- Road distances → Edge weights
- Starting city → Source
- Destination city → Goal

### Features

- Interactive source and destination selection
- Case-insensitive city input
- Shortest path calculation
- Total distance calculation
- Number of road segments
- Execution time measurement

### Algorithm

**Dijkstra's Shortest Path Algorithm**

### Complexity

With a binary heap:

```text
O((V + E) log V)
