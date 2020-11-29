** Maximum Multicommodity flow ** 

Work builds directly on the simple anlaysis done by Garg et al. 
Using the linear programming path formulation of the multicommodity flow problem.
Let P(i) = set of paths from s(i) to t(i) and 
Let P = Union of all P(i) 

The variable x(P) equals the amount of flow sent along path P.

*** Primal problem ***
maximise (Σ(p belongs to P)) x(P)
Constraints:
- for all e: (Σ(p:e belongs to P)) x(P) <= u(e)
- for all P: x(P) >= 0 

The dual LP problem is to assign lengths to the edges of the graph so that the length of the shortest parth from s(i) to t(i) is at least 1 for all commodities i. The length of an edge represents the marginal cost of using an additional unit of capacity of the edge.

*** Dual problem ***
minimize (Σ (e belongs to E)) u(e).l(e)
Constraints 
- for all P: (Σ (e belongs to P)) l(e) >= 1
- l(e) >= 0

*** The algorithm ***
- starts with length function l = σ for an appropriately defined σ depending on m and ε, and with a primal solution x = 0. 
- While there is a path in P of length less than 1, the algorithm selects such a path and augments flow along this path. 
- The amount of flow sent along path P is determined by the bottlenext capacity of the path, using the original capacities. (Denote this capacity by u)
- Primal solution is updated by setting x(P) = x(P) + u. This solution may be infeasible, since it will likely violate capacity constraints. (However it satisfies all other primal constraints)
- At the end of the algorithm, we will scale the final primal solution so that it is feasible. 
- After updating x(P), the dual variables are updated by increasing the lengths of the exponentially in relation to the congestion of the edge. For each edge e on P, the update is:
    l(e) = l(e) (1 + (ϵu / u(e)))
- The length of edges not on P remain unchanged.
- This update ensures the length of the bottleneck on P increases by a factor of (1 + ϵ).

**** Key to efficiency of algorithm **** 
Lies in the selection of P.
Garg et al show that if P = argmin(p ϵ P) l(P), where l(P) = Σ(e belongs to P) l(e), then the following lemmas hold:

![Lemmas](/Fleischer/images/lemmas-2.1-2.3.png)
