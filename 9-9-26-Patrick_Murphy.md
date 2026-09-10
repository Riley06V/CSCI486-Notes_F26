# Notes for 9/9/26

## Zero sum

**Zero sum:** If I win, you lose  
- aka utility(s, p1) + utility (s, p2) = c $\forall$ terminal states $s$

- `utility(s, p)`: score of player `p` in terminal state `s`
  - Example of score: win = `1`, loss = `-1`, draw = `0`
- `s0`: initial state
- `player(s)`: whose turn it is in state `s`
  - Example with tic-tac-toe: the board tells us whose turn comes next based on the number of X's and O's.
- `actions(s)`: all legal moves available in state `s`
- `result(s, a)`: result of action `a` in state `s`
- `terminal(s)`: whether `s` is a terminal/end state

For 2 player, zero sum games, utility(s) = utility(s,p)  
- **MAX is P1**, (maximizes utility)
- **MIN is P2**, (minimize utility(s) = c - utility (s,P2))


## Minimax Pseudocode
```text
Minimax(s):
    if TerminalTest(s):
        return Utility(s)

    if Player(s) == MAX:
        return max    Minimax(Result(s, a))

    if Player(s) == MIN:
        return min    Minimax(Result(s, a))
```

## Game tree utility

```text
                            (A)
                      /      |       \
                    a1      a2       a3
                   /         |          \
              (B)           (C)          (D)
             / |  \        / |  \       / |  \
           -2  2   2      0  0   1     1  1  -1
```
does max win? Is there advantage to going first/second?
> depends on the game. Some games it's better to go first and other games it's better to go second

## MAX / MIN
```text
                            (A)
                      /      |       \
                    a1      a2       a3
                   /         |          \
              (B)           (C)          (D)
             / |  \        / |  \       / |  \
            3  12  8      2  ?   ?     ?  ?   ?
                             ^
                              Does this matter?
```
> No. Because the the min of 'B' is 3 and C has a value of 2. Any value greater than 2 would not be considered 2 would always be the min in that case. And if the value is less than 2 then it wouldn't matter because 'B' 3 would always be greater than it. 

## Alpha-Beta Pseudocode

```text
function ALPHA-BETA-SEARCH(state) returns an action
    v <- MAX-VALUE(state, -infinity, +infinity)
    return the action in ACTIONS(state) with value v


function MAX-VALUE(state, alpha, beta) returns a utility value
    if TERMINAL-TEST(state) then return UTILITY(state)
    v <- -infinity
    for each a in ACTIONS(state) do
        v <- MAX(v, MIN-VALUE(RESULT(s, a), alpha, beta))
        if v >= beta then return v
        alpha <- MAX(alpha, v)
    return v


function MIN-VALUE(state, alpha, beta) returns a utility value
    if TERMINAL-TEST(state) then return UTILITY(state)
    v <- +infinity
    for each a in ACTIONS(state) do
        v <- MIN(v, MAX-VALUE(RESULT(s, a), alpha, beta))
        if v <= alpha then return v
        beta <- MIN(beta, v)
    return v
```