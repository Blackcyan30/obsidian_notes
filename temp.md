## Detecting an Odd Cycle in a Graph

The key observation is that a graph has an odd-length cycle if and only if it is not bipartite. Thus, we can use a breadth-first search (BFS) (or DFS) to try to two-color the graph. If at some point we find an edge connecting two vertices of the same color, the graph has an odd cycle.

### Pseudocode

function hasOddCycle(Graph G):
    // Initialize all vertices as uncolored
    for each vertex v in V(G):
        color[v] = UNCOLORED

    // Process each component of G
    for each vertex v in V(G):
        if color[v] == UNCOLORED:
            color[v] = RED
            initialize empty queue Q
            enqueue v into Q

            while Q is not empty:
                u = Q.dequeue()
                for each neighbor w of u:
                    if color[w] == UNCOLORED:
                        // Assign opposite color to w
                        color[w] = (color[u] == RED) ? BLUE : RED
                        enqueue w into Q
                    else if color[w] == color[u]:
                        // Found two adjacent vertices with the same color => odd cycle
                        return True

    // No conflicts found: graph is bipartite, so no odd cycle exists
    return False

### Time Complexity Derivation

- Initializing the color for all vertices takes $O(V)$ time.
- The BFS over each connected component processes each vertex and each edge once, resulting in $O(V+E)$ time overall.
- Therefore, the entire algorithm runs in $O(V+E)$ time.

### Simple Explanation

1. **Idea:**  
   A graph is bipartite if you can divide its vertices into two sets such that every edge connects a vertex in one set with a vertex in the other. If a graph is not bipartite, then it contains an odd cycle.

2. **How the Algorithm Works:**  
   - We start by marking all vertices as uncolored.
   - Then, for each uncolored vertex, we start a BFS, coloring it (say, RED) and then every neighbor BLUE.
   - When a vertex is encountered that is already colored, we check: if it has the same color as its neighbor from which it was reached, then there’s an edge connecting two vertices of the same color. This means the graph cannot be divided into two sets without conflict, implying an odd cycle exists.
   - If we complete the BFS for all vertices without finding such a conflict, the graph is bipartite (and has no odd cycle).

3. **Time Complexity:**  
   The algorithm goes through each vertex and edge only once, so its overall time is proportional to $O(V+E)$.

This pseudocode and explanation together provide an efficient solution to detect odd cycles in a graph.
