# CS50 AI — Lecture 0: Search

*Started: May 17, 2026 | Completed: May 18, 2026*

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

## Greedy Best-First Search

A search algorithm that expands the closest node to the goal as **estimated by a heuristic function `h(n)`**.
- We don't fully know the actual cost to the goal — we estimate it. That estimate is the **heuristic**.

### Heuristic Functions
- **Manhattan Distance:** the smallest number of vertical + horizontal steps needed to reach the goal (no diagonals).
- A heuristic is NOT a guarantee of how many steps it will actually take — it's an *estimate*.
- A node right next to the initial state will have a higher Manhattan distance number than a node right next to the goal.

### Is Greedy Best-First Optimal?
- **No.** Greedy Best-First is arbitrary in a similar way to DFS — it picks whichever node has the lowest heuristic value, without considering the cost already accumulated.
- It will commit to its estimated "best" direction even if a more optimal solution exists down a different path.
- It's "greedy" because it always picks the option that looks best *right now*, without re-evaluating.

---

## A* Search

A search algorithm that expands nodes with the lowest value of `g(n) + h(n)`.

- `g(n)` = the cost to reach node `n` (path cost so far)
- `h(n)` = the estimated cost from `n` to the goal (the heuristic)
- `f(n) = g(n) + h(n)` = total estimated cost of the path through node `n`

### A* vs. Greedy Best-First
- Greedy Best-First commits to its estimated lowest number and keeps going.
- **A\* re-evaluates** as path costs accumulate — if a path that initially looked promising starts costing too much, A* will switch to a better one.

### Is A* Optimal?
Only if:
1. **`h(n)` is admissible** — it never overestimates the true cost to the goal.
2. **`h(n)` is consistent** — for every node `n` and successor `n'` with step cost `c`:
   - `h(n) ≤ h(n') + c`
   - In other words: the heuristic at the current node should never be higher than (the heuristic at the successor + the cost of getting there).

---

## Adversarial Search

When an algorithm faces an opponent who is trying to *stop* it from reaching its goal.

- **Example:** Tic-Tac-Toe is an adversarial problem — there's an opponent trying to stop the AI from winning.
- Different from regular search because the environment isn't passive — it's actively working against you.

---

## Minimax

In a game of Tic-Tac-Toe:

| Outcome | Value |
|---------|-------|
| O wins | -1 |
| Tie (no winner) | 0 |
| X wins | +1 |

- **X = MAX player** → favors a higher number (+1)
- **O = MIN player** → favors a lower number (-1)

### How It Works
The AI has no preconceived notions of how a game like Tic-Tac-Toe works. We need to define:
- The game's states
- The available actions
- A function that returns whether a state is terminal (game over)
- A utility function that returns +1 / 0 / -1 for terminal states

**Minimax is recursive.** The AI thinks: "If I make this move, what will my opponent do? And after that move, what would I do next?" It walks through the entire game tree (or as much of it as it can), alternating perspectives between MAX and MIN at each level.

### The Game Tree
Tic-Tac-Toe (and games in general) can be represented as a **tree** — each node is a state, each branch is a possible move. Minimax explores this tree to find the optimal move from the current state.

### Minimax Pseudocode

Given a state `s`:
- **MAX picks** the action `a` in `Actions(s)` that produces the **highest** value of `MIN-VALUE(RESULT(s, a))`.
- **MIN picks** the action `a` in `Actions(s)` that produces the **smallest** value of `MAX-VALUE(RESULT(s, a))`.

### MAX-VALUE Function

```
function MAX-VALUE(state):
    if TERMINAL(state):
        return UTILITY(state)
    v = -∞
    for action in ACTIONS(state):
        v = MAX(v, MIN-VALUE(RESULT(state, action)))
    return v
```

### MIN-VALUE Function

```
function MIN-VALUE(state):
    if TERMINAL(state):
        return UTILITY(state)
    v = +∞
    for action in ACTIONS(state):
        v = MIN(v, MAX-VALUE(RESULT(state, action)))
    return v
```

> **Note:** MIN-VALUE starts at `+∞` (positive infinity) because MIN is trying to find the smallest value, so it needs to start high. MAX-VALUE starts at `-∞` because MAX is looking for the largest, so it needs to start low.

---

## Alpha-Beta Pruning

An optimization on top of minimax. The AI assumes the opponent is also playing optimally and uses that assumption to **skip evaluating branches** that won't affect the final decision.

- **Example:** if MAX is choosing between actions and already knows one branch guarantees a value of +5, it can stop exploring another branch the moment it sees that branch's MIN-VALUE could only give a result less than +5.
- This is "pruning" — cutting off branches of the game tree that can't possibly be better than what we've already found.
- Drastically reduces the number of states we evaluate without changing the final result.

Works great for Tic-Tac-Toe. For more complex games like chess, even with pruning, the tree is still too large to fully explore — so we need another optimization.

---

## Depth-Limited Minimax

Standard minimax explores the *entire* game tree until terminal states. For complex games (chess has ~10^120 possible states), that's impossible.

**Depth-Limited Minimax** caps the search at a fixed depth — explore N moves ahead, then stop.

### Evaluation Function
A function that **estimates the expected utility** of the game from a given non-terminal state.

- Instead of waiting until the game ends to assign +1/0/-1, an evaluation function looks at the current state and predicts how good it is.
- **Example:** in chess, an evaluation might return `0.8` to mean "white has a pretty good chance of winning from this position" — but it's not a guarantee.
- The quality of the evaluation function determines how well depth-limited minimax plays.

---

## Connections to Discrete Math

Search algorithms are essentially **applied graph theory** with a goal-finding twist.

- **Graph traversal** — BFS and DFS work on graphs of nodes and edges.
- **Shortest path problem** — what BFS solves on unweighted graphs.
- **Hamiltonian-style problems** — AI search generalizes the idea of visiting nodes to reach a destination (though it doesn't require visiting *every* node like a true Hamiltonian path).
- **NP-hardness** — the reason heuristics (A*) exist is because exhaustive search on large state spaces becomes computationally intractable, similar to why Traveling Salesman is hard.
- **Trees** — minimax is essentially recursive tree traversal with alternating perspectives at each level.

---

## Lecture Complete ✅

Up next: **Project 0** — Degrees (BFS) and Tic-Tac-Toe (Minimax).
