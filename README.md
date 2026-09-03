# Route-Finding---Part-1
Route-finding engine implementing DFS, BFS, Best-First Search, and A* on weighted map graphs, with performance analysis and standardized search metrics

# Route Finding Part 1

A graph-based route-finding engine that implements and compares four search strategies on weighted map graphs: **Depth-First Search, Breadth-First Search, Best-First Search, and A***.

The project explores how different graph search strategies navigate the same map while tracking path cost, heuristic values, evaluation functions, search depth, and frontier (OPEN-list) behavior.

## Features

* **Depth-First Search (DFS)** — explores nodes using a LIFO frontier.

* **Breadth-First Search (BFS)** — explores nodes using a FIFO frontier.

* **Best-First Search** — prioritizes nodes using the heuristic \(h(n)\).

* **A*** — prioritizes nodes using:

  $$
  f(n) = g(n) + h(n)
  $$

* Supports weighted map graphs with positive edge costs.

* Supports a single goal or multiple goal nodes.

* Uses **Straight-Line Distance (SLD)** as the heuristic for informed search.

* Maintains consistent node ordering and duplicate-handling policies across search strategies.

* Produces standardized search output and performance information.

* Supports optional visualization of search runs.

## Search Strategies

| Strategy    | Node Selection  | Evaluation      |
| ----------- | --------------- | --------------- |
| **DEPTH**   | LIFO            | \(g(n)\)        |
| **BREADTH** | FIFO            | \(g(n)\)        |
| **BEST**    | Lowest \(h(n)\) | \(h(n)\)        |
| **A***      | Lowest \(f(n)\) | \(g(n) + h(n)\) |

For informed searches, the heuristic is calculated using the Euclidean distance between the current node and the goal based on the coordinates provided in the map.

## Map Representation

Maps are represented as weighted graphs. Each edge contains:

```text
(node1, node2, edgevalue, [x1,y1], [x2,y2])
```

where:

* `node1`, `node2` — graph node labels
* `edgevalue` — positive edge/path cost
* `[x1,y1]`, `[x2,y2]` — node coordinates used for visualization and heuristic calculations

## Search Ordering

The implementation uses deterministic ordering rules to make the behavior of each algorithm reproducible.

### DFS

* Children are sorted alphabetically.
* Children are inserted at the front of OPEN.
* Uses LIFO ordering.

### BFS

* Children are sorted alphabetically.
* Children are inserted at the end of OPEN.
* Uses FIFO ordering.

### Best-First Search

* Nodes are ordered by ascending \(h(n)\).
* Alphabetical ordering is used to break heuristic ties.

### A*

* Nodes are ordered by ascending \(f(n)=g(n)+h(n)\).
* Ties are broken using lower \(g(n)\), followed by alphabetical node order.

Duplicate nodes in OPEN are handled according to the search strategy's evaluation policy, retaining the better candidate when applicable.

## Heuristic

The informed search strategies use **Straight-Line Distance (SLD)**:

$$
h(n) = \sqrt{(x_n-x_g)^2 + (y_n-y_g)^2}
$$

where \((x_n,y_n)\) represents the current node and \((x_g,y_g)\) represents the goal.

For A*:

$$
f(n)=g(n)+h(n)
$$

where \(g(n)\) is the accumulated path cost from the start node.

## Searcher Interface

The main interface is built around the `Searcher` class:

```python
Searcher(mapfile, searchType, verbose)
```

Set the start and goal:

```python
setStartGoal(startLabel, goalLabelOrList)
```

Execute the selected search:

```python
search()
```

Example:

```python
x = Searcher("10test.txt", searchType="A*", verbose=True)
x.setStartGoal("h", "k")
x.search()
```

## Example

For the sample `10test.txt` map, different search strategies can produce different routes.

For example, the A* search finds:

```text
['H', 'J', 'L', 'C', 'K']
```

while DFS and BFS may explore the graph differently before reaching the same goal.

This demonstrates the practical difference between **uninformed** and **heuristic-guided** graph search.

## Project Structure

```text
.
├── Searcher / search implementation
├── 06_tests.py
├── 10test.txt
├── 50test.txt
├── DRDViz.py
└── README.md
```

> File names may vary depending on the final repository organization.

## Running the Project

Clone the repository and run the test script:

```bash
git clone <repository-url>
cd <repository-directory>
python 06_tests.py
```

The project can be run against both provided maps:

* `10test.txt` — small map used for verbose step-by-step search analysis
* `50test.txt` — larger map used for summary-level comparison

## What This Project Demonstrates

This project focuses on practical implementation of **graph search and pathfinding algorithms**, including:

* Graph traversal
* Frontier/OPEN-list management
* Priority-based search
* Heuristic search
* Path-cost tracking
* Search-state management
* Deterministic algorithm behavior
* Algorithm comparison
* Route reconstruction

The same graph can be explored using fundamentally different search policies, providing a direct comparison of how search strategy affects the route discovered and the nodes explored.

## Visualization

The project can optionally be used with `DRDViz.py` to visualize map nodes, edges, and start/goal locations.

Visualization is supplementary to the core search engine and is not required for the search algorithms themselves.

---

### Technologies & Concepts

**Python · Graph Algorithms · Pathfinding · DFS · BFS · Best-First Search · A* · Heuristics · Weighted Graphs · Algorithm Analysis**
