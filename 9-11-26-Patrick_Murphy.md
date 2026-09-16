# AI Notes — 9/11/26

## Search Trees with Multiple Players

- Assume opponent is smart/rational.
- **MAX** = player
- **MIN** = opponent
- MAX wants highest score.
- MIN wants lowest score.

```text
        MAX
      /  |  \
    MIN MIN MIN
    / \  / \  / \
  MAX MAX MAX MAX MAX MAX
```

- MAX chooses `max(children)`
- MIN chooses `min(children)`

---

## Minimax

Minimax assumes both players play optimally.

```text
MAX → highest value
MIN → lowest value
```

Example:

```text
        MAX
       /   \
     MIN   MIN
    / \    / \
   5   2  8   4
```

```text
Left MIN = 2
Right MIN = 4
MAX = 4
```

---

## Alpha-Beta Pruning
Alpha-beta pruning avoids searching branches that cannot affect the final minimax answer.
It gives the **same result as minimax**, but can search fewer nodes.

### Alpha (α)
Best value MAX can guarantee so far.
```text
α = -∞
α = max(α, v)
```

### Beta (β)
Best value MIN can guarantee so far.
```text
β = +∞
β = min(β, v)
```
---

## MAX-VALUE

```text
function MAX-VALUE(state, α, β) returns a utility value
if TERMINAL-TEST(state) then return UTILITY(state)
v = -∞
for each a in ACTIONS(state) do
    v = max(v, MIN-VALUE(RESULT(s,a),α,β))
    if v ≥ β then return v
    α = max(α, v)
return v
```

## MIN-VALUE

```text
function MIN-VALUE(state, α, β) returns a utility value
if TERMINAL-TEST(state) then return UTILITY(state)
v = +∞
for each a in ACTIONS(state) do
    v = min(v, MAX-VALUE(RESULT(s,a),α,β))
    if v ≤ α then return v
    β = min(β, v)
return v
```
