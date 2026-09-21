# August 2026

## Introduction

### BFS vs. DFS Complexity

| Algorithm | Time | Space |
|-----------|------|-------|
| BFS | $O(b^d)$ | $O(b^d)$ |
| DFS | $O(b^M)$ | $O(bm)$ |

**Best of both worlds?**

---

## Iterative-Deepening DFS (IDDFS)

**Idea:** DFS is light on memory, but can overshoot the goal — limiting the depth and gradually increasing it fixes this.

### Iterative-Deepening Search Pseudo Code

```text
function Iterative-Deepening-Search(problem) returns a solution node or cutoff
    for depth = 0 to infinity do
        result <- Depth-Limited-Search(problem, depth)
        if result != cutoff then return result
```

*Note: make table.*

### IDDFS Properties

| Property | Result |
|----------|--------|
| Complete | Yes, unless branching factor $b$ is infinite |
| Optimal | Yes, if step costs are identical |
| Time | $O(b^d)$ |
| Space | $O(bd)$ |

---

## What if Steps Have Different Costs?

Let $E = \epsilon$.

### Best-First Search / Uniform Cost Search

This considers the cost to explore a path, and chooses the lowest-cost path first.

| Property | Result |
|----------|--------|
| Complete | Yes, if all step costs are above $\epsilon$ (costs keep decreasing for each step: $1, \tfrac{1}{2}, \tfrac{1}{4}, \dots$) |
| Optimal | Yes |
| Time | $O\left(b^{1 + \lfloor c/\epsilon \rfloor}\right)$ |
| Space | $O\left(b^{1 + \lfloor c/\epsilon \rfloor}\right)$ |

### Example: Cabins on a Hill

Trying to find rocks on a hill:

- Up cost: 5
- Side cost: 3
- Down cost: 1

If we know the cabin is near the top, we can direct our search.

---

## A\* Search

A\* searches "towards" a goal node.

Uses a **heuristic**: an estimate of the remaining cost to the goal.
