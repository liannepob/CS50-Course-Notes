# CS50 AI — Lecture 0: Search

*Started: May 17, 2026*

> Think about search problems like solving a maze on a map — finding a path from where you are to where you want to be.

---

## Search Problems

An AI navigating from point A to point B (a car, a maze solver, a game-playing engine) is solving a **search problem**. Every search problem has the same set of components:

### Agent
An entity that perceives its environment and acts upon that environment in some way.
- **Example:** a car trying to get to its destination on a map.

### State
A specific configuration the agent could be in.
- **Initial state:** the state where the agent begins — the start of the search algorithm.

### Actions
The choices that can be made in a given state.
- Recurring theme: we can define actions as a function.
- `actions(s)` returns the set of actions that can be executed in state `s`.

### Transition Model
A description of what state results from performing any applicable action.
- `result(s, a)` returns the state resulting from performing action `a` in state `s`.
- `s` represents the current state, `a` represents the action taken.

### State Space
The set of all states reachable from the initial state.
- Can be simplified into a **graph** with nodes (states) and arrows (actions that move between states).

### Goal Test
A way to determine whether a given state is a goal state.

### Path Cost
A numerical cost associated with a given path.
- We assign each path a cost so the AI takes the shortest/cheapest route.

### Solution
A sequence of actions that takes us from the initial state to a goal state.
- An **optimal solution** is the one with the lowest path cost.

---

## Nodes

A **node** is a data structure that keeps track of:

- A **state**
- A **parent** (the node that generated this one)
- An **action** (the action taken to get here)
- A **path cost**

---

## The Search Algorithm (Pseudocode)

How would we approach a search problem?

```
1. Start with a frontier containing the initial state.
2. Repeat:
    - If the frontier is empty → no solution.
    - Remove a node from the frontier.
    - If the node contains the goal state → return the solution.
    - Otherwise, expand the node (look at neighboring states) and
      add the resulting nodes to the frontier.
```

This is the pseudocode skeleton that gets translated into Python for the projects.

---

## Frontier Data Structures

The *type* of data structure used for the frontier determines the search algorithm.

### Stack (LIFO — Last In, First Out)
- **Depth-First Search (DFS):** expand the deepest node in the frontier first.

### Queue (FIFO — First In, First Out)
- **Breadth-First Search (BFS):** expand the shallowest node in the frontier first.

---

## DFS vs. BFS

**Example:** finding a path through a maze from A → B.

### Depth-First Search (DFS)
- Follows one path all the way to its end, then backtracks and tries another.
- **Not always optimal** — the starting direction is somewhat arbitrary, so it may find *a* path that isn't the shortest.

### Breadth-First Search (BFS)
- Explores all neighbors at the current depth before moving deeper.
- Expands outward from the initial state in waves.
- Slowly works its way to the target, level by level.

### Key Observation
- Both algorithms may explore extra states before reaching the goal.
- In most maze examples, **BFS finds a shorter path than DFS** because BFS commits to exploring evenly rather than diving down arbitrary paths.
- DFS's "arbitrary start" is what costs it optimality.

---

## Uninformed vs. Informed Search

### Uninformed Search
A strategy that uses **no problem-specific knowledge**.
- The algorithm has no idea where the goal is in the grid — it picks directions blindly.
- BFS and DFS are both uninformed.

### Informed Search
A strategy that uses **problem-specific knowledge** to find solutions more efficiently.
- **Example:** If I know point A is on the right side of the map and point B is somewhere on the left, I'm more likely to head left first — it feels like the "safer" option toward the goal.
- This intuition is what algorithms like A* formalize using **heuristic functions**.

---

## Connections to Discrete Math

Search algorithms are essentially **applied graph theory** with a goal-finding twist.

- **Graph traversal** — BFS and DFS work on graphs of nodes and edges.
- **Shortest path problem** — what BFS solves on unweighted graphs.
- **Hamiltonian-style problems** — AI search generalizes the idea of visiting nodes to reach a destination (though it doesn't require visiting *every* node like a true Hamiltonian path).
- **NP-hardness** — the reason heuristics (A*) exist is because exhaustive search on large state spaces becomes computationally intractable, similar to why Traveling Salesman is hard.

---

## Stopping Point

📍 **Stopped at 54:36 in the lecture.**

Next up: informed search (greedy best-first, A*) and adversarial search (minimax for game-playing AI).
