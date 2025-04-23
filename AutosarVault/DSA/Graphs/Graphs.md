Striver graphs: https://takeuforward.org/graph/striver-graph-series-top-graph-interview-questions

**Major types:**
1. [[BFS-DFS]]
2. [[Topological Sort]]
3. [[Shortest path algo]]
4. [[Minimum Spanning Tree - Disjoint Set]]
5. [[Other Graph Algo]]

- Degree of a node -> number of edges attached to that node
- Total degree of a graph is twice the number of edges for undirected graph.
- For directed graph, indegree is no. of incoming edges on a node.0

### Graph Representation
1. Adjacency Matrix
2. Adjacency List
**Adjacency Matrix** -> n * n matrix, where n is the number of nodes. matrix(i,j) == 1 means there is an edge btw i and j. For weighted edges, we put the weight of edge at index i, j.
**Adjacency List** -> `vector<int> adj[n+1]` . 
				For weighted edges, `vector< pair <int,int> > adjList[n+1];` 


### BFS
`// BFS from given source s`
`vector<int> bfs(vector<vector<int>>& adj)  {`
    `int V = adj.size();`
    
    `int s = 0; // source node` 
    `// create an array to store the traversal`
    `vector<int> res;`

    `// Create a queue for BFS`
    `queue<int> q;`  
    
    `// Initially mark all the vertices as not visited`
    `vector<bool> visited(V, false);`

    `// Mark source node as visited and enqueue it`
    `visited[s] = true;`
    `q.push(s);`

    `// Iterate over the queue`
    `while (!q.empty()) {`
      
        `// Dequeue a vertex from queue and store it`
        `int curr = q.front();`
        `q.pop();`
        `res.push_back(curr);`

        `// Get all adjacent vertices of the dequeued` 
        `// vertex curr If an adjacent has not been` 
        `// visited, mark it visited and enqueue it`
        `for (int x : adj[curr]) {`
            `if (!visited[x]) {`
                `visited[x] = true;`
                `q.push(x);`
            `}`
        `}`
    `}`

    `return res;`
`}`

****Time Complexity: O(V + E),**** BFS explores all the vertices and edges in the graph. In the worst case, it visits every vertex and edge once. Therefore, the time complexity of BFS is O(V + E), where V and E are the number of vertices and edges in the given graph.
****Auxiliary Space: O(V),**** BFS uses a queue to keep track of the vertices that need to be visited. In the worst case, the queue can contain all the vertices in the graph. 
This will not print all the nodes for an unconnected graph. For graph to print all the vertices, we need to call BFS from all the unvisited nodes of graph.
### DFS
`// Recursive function for DFS traversal`
`void dfsRec(vector<vector<int>> &adj, vector<bool> &visited, int s, vector<int> &res)`
`{`

    `visited[s] = true;`

    `res.push_back(s);`

    `// Recursively visit all adjacent vertices`
    `// that are not visited yet`
    `for (int i : adj[s])`
        `if (visited[i] == false)`
            `dfsRec(adj, visited, i, res);`
`}`

`// Main DFS function that initializes the visited array`
`// and call DFSRec`
`vector<int> DFS(vector<vector<int>> &adj)`
`{`
    `vector<bool> visited(adj.size(), false);`
    `vector<int> res;`
    `dfsRec(adj, visited, 0, res);`
    `return res;`
`}`

****Time complexity:**** O(V + E), where V is the number of vertices and E is the number of edges in the graph.  
****Auxiliary Space:**** O(V), since an extra visited array of size V is required, And stack size for recursive calls to dfsRec function.
This will not print all the nodes for an unconnected graph. For graph to print all the vertices, we need to call BFS from all the unvisited nodes of graph.