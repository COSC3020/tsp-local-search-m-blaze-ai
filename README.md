# Traveling Salesperson Problem -- Local Search

This exercise is about the Traveling Salesperson Problem I mentioned in the
lecture on NP-hard problems -- given a set of cities, determine the length of
the shortest tour that visits all of them. We can get from any city to any other
city, i.e. the graph of cities is completely connected. We consider the version
of the Traveling Salesperson Problem that finds the shortest tour to visit $n$
cities, starting at a city and ending at the $n$ th city; it *does not* go
back to the start. The start city may be any of the cities. Remember that the
graph for a TSP is undirected, i.e. the cost is the same in either direction.

The 2-opt algorithm for solving the Traveling Salesperson Problem is a
randomized local search algorithm that, at each iteration, reverses part of the
route. It starts with a random route (this is the randomized part), and changes
part of the route in each step (this is the local search part, sprinkled with
more randomness). The pseudocode for one iteration is as follows:

```javascript
2optSwap(route, i, k)
  cities 1 to i-1 stay in the order they are
  cities i to k are reversed
  cities k + 1 to n stay in the order they are
```

For example, if I call the above function with route A--B--C--D--E--F, $i=2$,
$k=4$, the resulting route is A--B--E--D--C--F.

The algorithm starts with a random route; if the new route at the end of an
iteration decreases the total length, it is retained as the current incumbent.
The incumbent after the final iteration is returned as the solution.

Implement the 2-opt algorithm, which repeatedly runs the above steps. Your
implementation needs to fix two design parameters that I have left open. First,
you need to design a stopping criterion -- when would it make sense to stop and
return the shortest route found so far rather than trying another iteration?
Second, design a way to choose $i$ and $k$ -- note that they need to be
different in subsequent iterations, as one iteration would simply undo what
the previous one did otherwise. Start with the template I provided in `code.js`.
Describe in your code how you designed your stopping criterion and ways of
choosing $i$ and $k$ and why.

The function takes a distance matrix (the adjacency matrix for the graph where
the values in the cells are the distances between the corresponding cities) and
returns the length of the shortest tour (not the tour itself).

Test your new function; I've provided some basic testing code in `code.test.js`.

## Runtime Analysis

What is the worst-case asymptotic time complexity of your implementation? What
is the worst-case asymptotic memory complexity? Add your answer, including your
reasoning, to this markdown file.

Worst-case time:
Number of vertices/nodes (cities) = n
Initial tour generation (randomized) = $\Theta$(n) time
2-OptSwap & Tour length recalculation = $\Theta$(n) time
worst case iterations = 1000

worst case time = $\Theta(1000 \times n) = \Theta(n)$

worst-case space = $\Theta(n^2)$


The worst-case time complexity is $\Theta(n^2)$, where n is the number of cities. This is because he algorithm starts with generating an initial random tour (usually done at setup), which typically takes $\Theta$(n) time. Then, during each iteration, the algorithm does a 2-opt swap and recalculates the tour length, both taking $\Theta$(n) time. With up to 1000 iterations in the worst case, the worst-case time complexity is $\Theta(n^2)$.

The worst-case space complexity is $\Theta(n)$, with n being the number of cities. This is due to the fact that the algorithm saves the current tour as a list of cities, which requires linear space. Additionally, during each iteration, a temporary list can be used to hold a potential tour after the 2-opt swap is performed, which also uses linear space. Since no other data structures were used, the overall space use remains proportional to the cities.



“I certify that I have listed all sources used to complete this exercise, including the use
of any Large Language Models. All of the work is my own, except where stated
otherwise. I am aware that plagiarism carries severe penalties and that if plagiarism is
suspected, charges may be filed against me without prior notice.”

For this assignment, I asked Chat GPT for help improving my reasoning, mostly regarding its presentation and articulation. I also recieved help from Chat GPT with troubleshooting errors in my code.js file.