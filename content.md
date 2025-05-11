Topic: Greedy Algorithms    
Overview    
Greedy algorithms build up a solution step-by-step, always choosing the option that looks best at the moment. They don’t reconsider decisions later, which makes them fast and simple, but only correct for problems where a greedy choice leads to an optimal solution. Typical applications include activity selection, Huffman coding, coin change, minimum spanning trees, and shortest paths.

Greedy Choice Property    
To use a greedy approach, the problem must exhibit the “greedy choice property”:  

- A global optimal solution can be reached by making a locally optimal choice at each step.

Optimal Substructure    
Greedy algorithms also require “optimal substructure”:  

- An optimal solution to the problem contains optimal solutions to subproblems.

This property is shared with dynamic programming, but greedy algorithms make decisions once and don’t revise them, unlike DP which explores all possibilities.

Classic Examples

- Activity Selection  

Choose the maximum number of activities that don’t overlap. Sort activities by finish time and always pick the next one that starts after the last selected activity.

- Fractional Knapsack  

You are given a set of items, each with a weight and a value. Your goal is to choose a subset of these items to maximize total value without exceeding a fixed weight capacity of a knapsack. You can take parts of items. Sort by value-to-weight ratio and take as much as you can of the highest ratios.

- Minimum Spanning Tree  

Greedy works perfectly:  
\- Kruskal’s Algorithm: Sort edges by weight, add to tree if they don’t form a cycle.  
\- Prim’s Algorithm: Grow the MST by always adding the smallest edge connecting a visited and unvisited node.  
     \-     Dijkstra’s Algorithm    
Finds shortest paths from a single source in graphs with non-negative weights. Uses a priority queue to always expand the nearest unvisited node.

When Greedy algorithm does not work:  
Greedy fails when early decisions block better long-term outcomes.  
Examples:  

1. In the coin change problem:  
   1. a greedy algorithm may not give the minimum number of coins if the denominations are unusual  
      For instance, \[1, 3, 4\] and amount \= 6 → greedy picks 4+1+1 \= 3 coins, optimal is 3+3 \= 2 coins.  
2. 0/1 Knapsack  
   1. Now you can’t break items, since you either take the whole thing or skip.  
      Item	Value	Weight	  
      A	60	10	  
      B	100	20	  
      C	120	50	  
      With capacity \= 50, greedy algorithm will take Item C with Value=120 only, however items A and B in sum give 160\.

How to find out if a greedy algorithm works in your case?  (Proving correctness)  
To prove a greedy algorithm is correct:

1. Show the “greedy choice property” holds.  
2. Prove “optimal substructure”.  
3. Additionally: exchange argument:  
   Show that any optimal solution can be transformed into the greedy one without loss. Imagine Activity Selection. Your greedy plan says: Always pick the one that ends earliest. Now someone else has a different plan. If you swap their first activity with mine (which ends earlier), the rest still will fit. So the greedy solution is also optimal.

Key Takeaways    
\- Greedy algorithms make decisions step-by-step with no backtracking.  
\- Only work when greedy choices yield optimal solutions.  
\- Use exchange arguments or induction to prove correctness.  
\- Good for problems like MSTs, scheduling, and Dijkstra’s algorithm.

