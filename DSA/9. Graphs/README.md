# 🌐 Graphs - Connected Data Structures

Welcome to the **Graphs** section! Master graph algorithms that model real-world relationships and solve complex connectivity problems.

---

## 📚 What is a Graph?

A **Graph** is a collection of vertices (nodes) connected by edges, representing relationships between entities.

**Components**:
- **Vertices (V)**: Nodes or points in the graph
- **Edges (E)**: Connections between vertices
- **Weight**: Optional value associated with edges
- **Path**: Sequence of vertices connected by edges

---

## 🔧 Graph Types

### 🎯 By Direction
- **Undirected**: Edges have no direction (friendship network)
- **Directed**: Edges have direction (web page links)

### ⚖️ By Weight
- **Unweighted**: All edges have equal importance
- **Weighted**: Edges have associated costs/distances

### 🔗 By Connectivity
- **Connected**: Path exists between every pair of vertices
- **Disconnected**: Some vertices are unreachable

### 🎭 Special Types
- **Tree**: Connected acyclic graph (n-1 edges for n vertices)
- **DAG**: Directed Acyclic Graph (topological ordering possible)
- **Complete**: Every vertex connected to every other vertex

---

## 🏗️ Graph Representation

### 1. Adjacency Matrix
```java
class GraphMatrix {
    private int[][] adjMatrix;
    private int vertices;
    
    public GraphMatrix(int v) {
        vertices = v;
        adjMatrix = new int[v][v];
    }
    
    public void addEdge(int src, int dest) {
        adjMatrix[src][dest] = 1;
        adjMatrix[dest][src] = 1; // For undirected graph
    }
    
    public boolean hasEdge(int src, int dest) {
        return adjMatrix[src][dest] == 1;
    }
}
```
**Pros**: O(1) edge lookup, good for dense graphs  
**Cons**: O(V²) space, O(V²) initialization

### 2. Adjacency List
```java
class GraphList {
    private List<List<Integer>> adjList;
    private int vertices;
    
    public GraphList(int v) {
        vertices = v;
        adjList = new ArrayList<>();
        for (int i = 0; i < v; i++) {
            adjList.add(new ArrayList<>());
        }
    }
    
    public void addEdge(int src, int dest) {
        adjList.get(src).add(dest);
        adjList.get(dest).add(src); // For undirected graph
    }
    
    public List<Integer> getNeighbors(int vertex) {
        return adjList.get(vertex);
    }
}
```
**Pros**: O(V + E) space, efficient for sparse graphs  
**Cons**: O(degree) edge lookup

---

## 🚶 Graph Traversal Algorithms

### 1. Depth-First Search (DFS)
```java
public void dfs(int vertex, boolean[] visited, List<List<Integer>> adjList) {
    visited[vertex] = true;
    System.out.print(vertex + " ");
    
    for (int neighbor : adjList.get(vertex)) {
        if (!visited[neighbor]) {
            dfs(neighbor, visited, adjList);
        }
    }
}
```
**Time**: O(V + E) | **Space**: O(V) | **Use**: Cycle detection, topological sort

### 2. Breadth-First Search (BFS)
```java
public void bfs(int start, List<List<Integer>> adjList) {
    boolean[] visited = new boolean[adjList.size()];
    Queue<Integer> queue = new LinkedList<>();
    
    visited[start] = true;
    queue.offer(start);
    
    while (!queue.isEmpty()) {
        int vertex = queue.poll();
        System.out.print(vertex + " ");
        
        for (int neighbor : adjList.get(vertex)) {
            if (!visited[neighbor]) {
                visited[neighbor] = true;
                queue.offer(neighbor);
            }
        }
    }
}
```
**Time**: O(V + E) | **Space**: O(V) | **Use**: Shortest path, level-order traversal

---

## 🛣️ Shortest Path Algorithms

### 1. Dijkstra's Algorithm (Single Source, Non-negative weights)
```java
public int[] dijkstra(int src, int vertices, List<List<int[]>> graph) {
    int[] dist = new int[vertices];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;
    
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.offer(new int[]{src, 0});
    
    while (!pq.isEmpty()) {
        int[] current = pq.poll();
        int u = current[0];
        
        for (int[] edge : graph.get(u)) {
            int v = edge[0], weight = edge[1];
            
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.offer(new int[]{v, dist[v]});
            }
        }
    }
    
    return dist;
}
```

### 2. Bellman-Ford Algorithm (Single Source, Negative weights)
```java
public boolean bellmanFord(int src, int vertices, List<int[]> edges) {
    int[] dist = new int[vertices];
    Arrays.fill(dist, Integer.MAX_VALUE);
    dist[src] = 0;
    
    // Relax edges V-1 times
    for (int i = 0; i < vertices - 1; i++) {
        for (int[] edge : edges) {
            int u = edge[0], v = edge[1], weight = edge[2];
            if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
            }
        }
    }
    
    // Check for negative cycles
    for (int[] edge : edges) {
        int u = edge[0], v = edge[1], weight = edge[2];
        if (dist[u] != Integer.MAX_VALUE && dist[u] + weight < dist[v]) {
            return false; // Negative cycle exists
        }
    }
    
    return true;
}
```

### 3. Floyd-Warshall Algorithm (All Pairs)
```java
public int[][] floydWarshall(int[][] graph) {
    int V = graph.length;
    int[][] dist = new int[V][V];
    
    // Initialize distances
    for (int i = 0; i < V; i++) {
        for (int j = 0; j < V; j++) {
            dist[i][j] = graph[i][j];
        }
    }
    
    // Find shortest paths
    for (int k = 0; k < V; k++) {
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (dist[i][k] + dist[k][j] < dist[i][j]) {
                    dist[i][j] = dist[i][k] + dist[k][j];
                }
            }
        }
    }
    
    return dist;
}
```

---

## 🌳 Minimum Spanning Tree

### 1. Kruskal's Algorithm
```java
public int kruskal(int vertices, List<int[]> edges) {
    // Sort edges by weight
    edges.sort((a, b) -> a[2] - b[2]);
    
    UnionFind uf = new UnionFind(vertices);
    int mstWeight = 0;
    int edgesUsed = 0;
    
    for (int[] edge : edges) {
        int u = edge[0], v = edge[1], weight = edge[2];
        
        if (uf.find(u) != uf.find(v)) {
            uf.union(u, v);
            mstWeight += weight;
            edgesUsed++;
            
            if (edgesUsed == vertices - 1) break;
        }
    }
    
    return mstWeight;
}
```

### 2. Prim's Algorithm
```java
public int prim(int vertices, List<List<int[]>> graph) {
    boolean[] inMST = new boolean[vertices];
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    
    pq.offer(new int[]{0, 0}); // {vertex, weight}
    int mstWeight = 0;
    
    while (!pq.isEmpty()) {
        int[] current = pq.poll();
        int vertex = current[0], weight = current[1];
        
        if (inMST[vertex]) continue;
        
        inMST[vertex] = true;
        mstWeight += weight;
        
        for (int[] edge : graph.get(vertex)) {
            int neighbor = edge[0], edgeWeight = edge[1];
            if (!inMST[neighbor]) {
                pq.offer(new int[]{neighbor, edgeWeight});
            }
        }
    }
    
    return mstWeight;
}
```

---

## 🔄 Cycle Detection

### In Undirected Graph (DFS)
```java
public boolean hasCycleDFS(int vertex, int parent, boolean[] visited, 
                          List<List<Integer>> adjList) {
    visited[vertex] = true;
    
    for (int neighbor : adjList.get(vertex)) {
        if (!visited[neighbor]) {
            if (hasCycleDFS(neighbor, vertex, visited, adjList)) {
                return true;
            }
        } else if (neighbor != parent) {
            return true; // Back edge found
        }
    }
    
    return false;
}
```

### In Directed Graph (DFS with colors)
```java
public boolean hasCycleDirected(int vertex, int[] color, List<List<Integer>> adjList) {
    color[vertex] = 1; // Gray (visiting)
    
    for (int neighbor : adjList.get(vertex)) {
        if (color[neighbor] == 1) return true; // Back edge
        if (color[neighbor] == 0 && hasCycleDirected(neighbor, color, adjList)) {
            return true;
        }
    }
    
    color[vertex] = 2; // Black (visited)
    return false;
}
```

---

## 📊 Topological Sorting

### DFS-based Approach
```java
public List<Integer> topologicalSort(int vertices, List<List<Integer>> adjList) {
    boolean[] visited = new boolean[vertices];
    Stack<Integer> stack = new Stack<>();
    
    for (int i = 0; i < vertices; i++) {
        if (!visited[i]) {
            topSortDFS(i, visited, adjList, stack);
        }
    }
    
    List<Integer> result = new ArrayList<>();
    while (!stack.isEmpty()) {
        result.add(stack.pop());
    }
    
    return result;
}

private void topSortDFS(int vertex, boolean[] visited, 
                       List<List<Integer>> adjList, Stack<Integer> stack) {
    visited[vertex] = true;
    
    for (int neighbor : adjList.get(vertex)) {
        if (!visited[neighbor]) {
            topSortDFS(neighbor, visited, adjList, stack);
        }
    }
    
    stack.push(vertex);
}
```

### Kahn's Algorithm (BFS-based)
```java
public List<Integer> kahnsAlgorithm(int vertices, List<List<Integer>> adjList) {
    int[] indegree = new int[vertices];
    
    // Calculate indegrees
    for (int i = 0; i < vertices; i++) {
        for (int neighbor : adjList.get(i)) {
            indegree[neighbor]++;
        }
    }
    
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < vertices; i++) {
        if (indegree[i] == 0) {
            queue.offer(i);
        }
    }
    
    List<Integer> result = new ArrayList<>();
    
    while (!queue.isEmpty()) {
        int vertex = queue.poll();
        result.add(vertex);
        
        for (int neighbor : adjList.get(vertex)) {
            indegree[neighbor]--;
            if (indegree[neighbor] == 0) {
                queue.offer(neighbor);
            }
        }
    }
    
    return result.size() == vertices ? result : new ArrayList<>();
}
```

---

## 🔗 Union-Find (Disjoint Set Union)
```java
class UnionFind {
    private int[] parent, rank;
    
    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }
    }
    
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Path compression
        }
        return parent[x];
    }
    
    public void union(int x, int y) {
        int rootX = find(x), rootY = find(y);
        if (rootX != rootY) {
            if (rank[rootX] < rank[rootY]) {
                parent[rootX] = rootY;
            } else if (rank[rootX] > rank[rootY]) {
                parent[rootY] = rootX;
            } else {
                parent[rootY] = rootX;
                rank[rootX]++;
            }
        }
    }
    
    public boolean connected(int x, int y) {
        return find(x) == find(y);
    }
}
```

---

## 🌟 Real-World Applications

### 🗺️ Navigation & Routing
- **GPS Systems**: Shortest path algorithms
- **Social Networks**: Friend recommendations, community detection
- **Internet**: Routing protocols, network topology

### 🏢 Computer Science
- **Compiler Design**: Dependency graphs, optimization
- **Operating Systems**: Process scheduling, deadlock detection
- **Database Systems**: Query optimization, transaction dependencies

### 🎯 Problem-Solving Patterns

| Pattern | Algorithm | Use Case |
|---------|-----------|----------|
| **Connectivity** | DFS/BFS | Connected components |
| **Shortest Path** | Dijkstra, BFS | Navigation, network routing |
| **Cycle Detection** | DFS, Union-Find | Deadlock detection |
| **Ordering** | Topological Sort | Task scheduling |
| **Minimum Cost** | MST algorithms | Network design |

---

## 🎯 Interview Preparation

### 🔥 Must-Know Problems
1. **Graph Valid Tree** - Cycle detection + connectivity
2. **Number of Islands** - Connected components with DFS/BFS
3. **Course Schedule** - Topological sorting and cycle detection
4. **Word Ladder** - BFS shortest path
5. **Network Delay Time** - Dijkstra's algorithm
6. **Minimum Spanning Tree** - Kruskal's or Prim's
7. **Clone Graph** - DFS/BFS with node creation

### 💡 Key Concepts
- **Graph representation** trade-offs
- **Traversal algorithms** and their applications
- **Shortest path** algorithm selection
- **Cycle detection** in directed vs undirected graphs
- **Topological sorting** and its prerequisites

---

**Ready to explore graph algorithms?** Check out [Problems.md](./Problems.md) for hands-on practice! 🌐