# Monday September 7th

## Selecting a Heuristic
1. Relax Problem
	- EX. 8 Puzzle
		1.sum of tiles dist(tile, goal position)
		sum of tiles adjusted_dist(tile, goal position)
			8 puzzle + we can move tiles on top of each other.
			8 puzzle + we can teleport tiles.
				sum of tiles 1(is tile in the right place)
				# of misplaced tiles

2. Pattern Database
	-EX. Solve subproblem + store exact results
		expensive to pre compute cost amortized.

3. Combine known heuristics
	- How to combine and maintain admissibility/consistency

Learn one from experience or from data.

## Weighted A*
h'(n) = w * h(n)
	expand fewer nodes
	return path with cost <= wC*

Bidirectional Search: starts at both the start position and goal position. It terminates when the searches meet.

## Too Big
How to search with multiple players?
	DFS, but doesn't find "the" solution.

										A
									/   |   \
								   B     C      D
								 / | \  /|\    /|\
							   -2 2  2  0 0 1  1 1 -1

	(What path should Player 1 choose?)
