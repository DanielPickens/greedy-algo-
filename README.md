# greedy-algo-
My solution for algo

Solves this algo: 






3. Greedy Approach
The difference between greedy and dynamic approach is that the DP solves subproblems first, then uses those solutions to make an optimal choice whereas Greedy makes an optimal choice (without knowing solutions to subproblems) and then solve remaining subproblem(s), but both apply to problems with optimal substructure.

Here, the problem only asks for the min number of jumps. So we do not have to figure out each jump position. We only need to store the max_reach of the previous jump position. If we go beyond that, we need one more jump.
