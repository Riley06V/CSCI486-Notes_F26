# Mon August 31st

## Recall: A\*

A\* searches "towards" a goal node.

### Heuristics

- **Heuristic:** an estimate of the path cost from a node to the goal.

$$h(n) = c$$

- **Restrictions:**
  - Non-negative
  - $h(G) = 0$ at the goal state
- **Euclidean distance:** distance measured on a flat plane.

### Greedy Best-First Search

Changes how we store the frontier so that $f = h$ (the heuristic). Chooses a path based on distance to the goal — the closer a node is to the goal, the more likely it is chosen.

### A\*

$$f(n) = g(n) + h(n)$$

"The cost so far + the estimated remaining cost"

---

## Does A\* Always Return the Optimal Path?

*Note: the diagram below is transcribed as closely as possible to the original hand-drawn version — worth double-checking against your notes/photo of the board if the numbers look off.*

```text
A --1--> B --1--> C --1--> D
 \                          | 1
  \----------5----------->  G

h(B) = h(C) = h(D) = 50        h(G) = 0
```

Going straight from $A$ to $G$ gives $f = 55$ because of the heuristic value (5), even though the other path (through $B$, $C$, $D$) may actually be cheaper.

---

## What Values of $h(B)$ Lead to an Optimal Solution?

*Note: same caveat as above — transcribed as closely as possible to the original diagram.*

```text
G1 --6--> A --3--> B

           |
           G2          h(goal) = 0
```

- **Question:** What values of $h(B)$ will lead to an optimal solution?
- **Answer:** $h(B) = 1$, since $2 + 1 = 3$, which is cheaper than $6$.

---

## Admissibility

- **Admissible heuristic:**

$$h(n) \le h^\ast(n)$$

  i.e., less than or equal to the true cost. This is "optimistic" — it underestimates the true cost.

### Proof Sketch: Admissible $h$ $\implies$ Tree A\* is Optimal

1. Suppose A\* is *not* optimal.
2. Then we pop a suboptimal goal node $G$ before the optimal node $G^\ast$.
3. Before we popped $G$, $G^\ast$ (or a node on the path to $G^\ast$) was on the frontier.

**Case 1: $G^\ast$ is also on the frontier.**
- Then we should have popped $G^\ast$ instead — contradiction.

**Case 2: $G^\ast$ is not on the frontier**, but some node $n$ on the path to $G^\ast$ is on the frontier.

- We pop $n$ before $G$, since

$$f(n) = g(n) + h(n)$$

  (priority = cost so far + estimated cost remaining), and

$$f(n) \le f(G^\ast) = g(G^\ast) \le g(G) = f(G)$$

*Note: the last line was cleaned up from the original — it had "$f(n) \le g(G^\ast) < g(G^\ast) = f(G)$," which repeats $g(G^\ast)$ and looks like a transcription slip. The corrected chain uses $h(G^\ast) = h(G) = 0$ at goal nodes, so $f(G^\ast) = g(G^\ast)$ and $f(G) = g(G)$, and $g(G^\ast) \le g(G)$ since $G^\ast$ is optimal.*
