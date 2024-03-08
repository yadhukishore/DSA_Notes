# Graphs
## Basic implementations
```javascript
class Graph {
    constructor() {
        this.vertices = {}; // Hash table to store vertices and their corresponding edges
    }

    // Method to insert a vertex and its edge(s) into the graph
    insert(vertex, edge, isBidirectional = true) {
        if (!this.vertices[vertex]) {
            this.vertices[vertex] = []; // Create an array to store edges for the new vertex
        }
        // Add the edge to the vertex's array
        this.vertices[vertex].push(edge);

        if (isBidirectional) {
            // If bidirectional, add the vertex as an edge to the destination vertex
            if (!this.vertices[edge]) {
                this.vertices[edge] = [];
            }
            this.vertices[edge].push(vertex);
        }
    }

    // Method to print the graph
    printGraph(){
        for(const vertex in this.vertices){
            const edges = this.vertices[vertex];
            console.log(`Vertex:${vertex}---> Edges:${edges.join(' , ')}`);
        }
    }
}

// Example usage:
const graph = new Graph();
graph.insert(3, 5, true);
graph.insert(3, 4, true);
graph.insert(5, 6, false);

graph.printGraph();
```
**Working**



1. **Check if the Vertex Exists**: First, we check if the vertex (node) already exists in the graph. If not, we initialize it in the graph by creating an empty array to store its edges.

2. **Add Edge to the Vertex**: We then add the edge (connection to another node) to the vertex's array of edges. This indicates that there is a connection between the vertex and the edge.

3. **Handle Bidirectional Connection**: If the connection is bidirectional (meaning it goes both ways), we add the vertex as an edge to the destination vertex as well. This ensures that the graph is properly connected in both directions.

Let's consider an example:

Suppose we have a graph where vertex `3` is connected to edge `5`, and it's bidirectional. Here's how the `insert()` method works:

- We check if vertex `3` exists. Since it doesn't initially, we create a new array for vertex `3` and add `5` as its edge.
- If bidirectional, we also check if vertex `5` exists. If not, we create a new array for vertex `5` and add `3` as its edge.

This process ensures that both vertices and edges are properly stored in the graph, allowing us to represent the connections between nodes accurately.
# BFS

```javascript
class Graph {
    constructor() {
        this.vertices = {};
    }

    insert(vertex, edge, isBidir = true) {
        if (!this.vertices[vertex]) {
            this.vertices[vertex] = [];
        }
        this.vertices[vertex].push(edge);

        if (isBidir) {
            if (!this.vertices[edge]) {
                this.vertices[edge] = [];
            }
            this.vertices[edge].push(vertex);
        }
    }

    bfs(source) {
        const visited = {}; // To keep track of visited nodes
        const queue = [source]; // Initialize queue with the source node

        visited[source] = true; // Mark source node as visited

        while (queue.length) {
            const currentVertex = queue.shift(); // Dequeue the first node
            console.log(currentVertex); // Process current node

            // Enqueue all unvisited neighbors
            this.vertices[currentVertex].forEach(neighbor => {
                if (!visited[neighbor]) {
                    visited[neighbor] = true; // Mark neighbor as visited
                    queue.push(neighbor); // Enqueue neighbor
                }
            });
        }
    }
}

// Example usage:
const graph = new Graph();
graph.insert(1, 2);
graph.insert(1, 3);
graph.insert(2, 4);
graph.insert(2, 5);
graph.insert(3, 6);

graph.bfs(3); // Start BFS from node 1

```
Of course! Let's break down the `bfs()` method in simple terms:

### Breadth-First Search (BFS) Method:

1. **Initialize Data Structures**:
   - Create an empty object called `visited` to keep track of visited nodes.
   - Create a queue (FIFO - First In, First Out) to store nodes to be visited next. Initially, enqueue the source node (starting node) into the queue.

2. **Start BFS**:
   - While the queue is not empty, continue the BFS process.

3. **Dequeue a Node**:
   - Dequeue (remove) the first node from the queue. This node represents the current node being processed.

4. **Process Current Node**:
   - Process the current node, which means performing any operations or tasks related to the node. In BFS, this typically involves visiting or exploring the node.

5. **Explore Neighbors**:
   - For each unvisited neighbor of the current node, mark it as visited and enqueue it into the queue. This step ensures that neighboring nodes are visited in a breadth-first manner, meaning nodes at the same level are visited before moving to the next level.

6. **Repeat Until Completion**:
   - Repeat steps 3 to 5 until all reachable nodes in the graph are visited. This ensures that BFS explores all nodes in the graph systematically, starting from the source node and moving outward layer by layer.

### Example:

Let's use the following graph as an example:

```
     1
    / \
   2   3
  / \   \
 4   5   6
```

Suppose we start BFS from node `1`. Here's how the algorithm proceeds:

1. **Initialization**:
   - `visited`: `{}` (empty object)
   - `queue`: `[1]` (contains source node)

2. **Iteration 1**:
   - Dequeue `1`.
   - Process `1`.
   - Enqueue unvisited neighbors `2` and `3`.

3. **Iteration 2**:
   - Dequeue `2`.
   - Process `2`.
   - Enqueue unvisited neighbor `4`.

4. **Iteration 3**:
   - Dequeue `3`.
   - Process `3`.
   - Enqueue unvisited neighbor `6`.

5. **Iteration 4**:
   - Dequeue `4`.
   - Process `4`.
   - No unvisited neighbors to enqueue.

6. **Iteration 5**:
   - Dequeue `5`.
   - Process `5`.
   - No unvisited neighbors to enqueue.

7. **Iteration 6**:
   - Dequeue `6`.
   - Process `6`.
   - No unvisited neighbors to enqueue.

8. **Completion**:
   - All reachable nodes are visited.

### Implementation in Code:

Here's the BFS method implemented in JavaScript:

```javascript
bfs(source) {
    const visited = {}; // To keep track of visited nodes
    const queue = [source]; // Initialize queue with the source node

    visited[source] = true; // Mark source node as visited

    while (queue.length) {
        const currentVertex = queue.shift(); // Dequeue the first node
        console.log(currentVertex); // Process current node

        // Enqueue all unvisited neighbors
        this.vertices[currentVertex].forEach(neighbor => {
            if (!visited[neighbor]) {
                visited[neighbor] = true; // Mark neighbor as visited
                queue.push(neighbor); // Enqueue neighbor
            }
        });
    }
}
```

This code snippet demonstrates how the BFS algorithm works and how it can be implemented in JavaScript. It follows the steps outlined above to explore the graph in a breadth-first manner.

# DFS
Absolutely! Let's delve into Depth-First Search (DFS), another fundamental graph traversal algorithm.

### Depth-First Search (DFS) Algorithm:

DFS explores as far as possible along each branch before backtracking. It traverses as deep as possible down one path before exploring adjacent vertices. The algorithm follows these steps:

1. **Start at the Source Node**: Begin DFS from a specific source node (starting node).

2. **Explore Neighbors**: Visit an unvisited neighbor of the current node and repeat the process recursively.

3. **Backtrack**: If all neighbors of a node have been visited, backtrack to the previous node and explore its unvisited neighbors.

4. **Repeat Until Completion**: Repeat steps 2 and 3 until all reachable nodes from the source node are visited.

DFS can be implemented using either recursion (recursive DFS) or a stack (iterative DFS).

### Implementation of DFS (Recursive Approach):

Here's a simple implementation of DFS using recursion in JavaScript:

```javascript
dfs(source, visited = {}) {
    visited[source] = true; // Mark source node as visited
    console.log(source); // Process current node

    // Explore all unvisited neighbors recursively
    this.vertices[source].forEach(neighbor => {
        if (!visited[neighbor]) {
            this.dfs(neighbor, visited);
        }
    });
}
```

### Implementation of DFS (Iterative Approach using Stack):

Here's an iterative implementation of DFS using a stack in JavaScript:

```javascript
dfs(source) {
    const visited = {}; // To keep track of visited nodes
    const stack = [source]; // Initialize stack with the source node

    while (stack.length) {
        const currentVertex = stack.pop(); // Pop the top node from the stack
        if (!visited[currentVertex]) {
            visited[currentVertex] = true; // Mark current node as visited
            console.log(currentVertex); // Process current node

            // Push unvisited neighbors onto the stack
            this.vertices[currentVertex].forEach(neighbor => {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            });
        }
    }
}
```

### Example:

Consider the following graph:

```
     1
    / \
   2   3
  / \   \
 4   5   6
```

Suppose we start DFS from node `1`. Here's how the algorithm proceeds:

1. **DFS (Recursive Approach)**:
   - Visit node `1`, then visit node `2`, then visit node `4`, and backtrack to node `2` to visit node `5`. Continue until all reachable nodes are visited.

2. **DFS (Iterative Approach)**:
   - Start at node `1`, then visit node `2`, then node `4`. Backtrack to node `2` to visit node `5`, then backtrack to node `1` to visit node `3` and node `6`.

DFS explores the graph deeply before backtracking, resulting in traversal along each branch until it reaches the end before exploring other branches.

# Remove vertex from graph?

```javascript
class Graph {
    constructor() {
        this.vertices = {};
    }

    insert(vertex, edge, isBidir = true) {
        if (!this.vertices[vertex]) {
            this.vertices[vertex] = [];
        }
        this.vertices[vertex].push(edge);

        if (isBidir) {
            if (!this.vertices[edge]) {
                this.vertices[edge] = [];
            }
            this.vertices[edge].push(vertex);
        }
    }

removeVertex(vertex) {

    for(const v in this.vertices){
        this.vertices[v]=this.vertices[v].filter(edge =>{
            if(edge === vertex){
                console.log(`Removing edge from vertex ${v} to vertex ${vertex}`);
                return false
            }
            return true;
        })
    }
    delete this.vertices[vertex];
    
}

    printGraph() {
        for (const vertex in this.vertices) {
            const edges = this.vertices[vertex];
            console.log(`Vertex:${vertex}---> Edges:${edges.join(' , ')}`);
        }
    }
}

// Example usage:
const graph = new Graph();
graph.insert(3, 5, true);
graph.insert(3, 4, true);
graph.insert(5, 6, false);

console.log("Before removal:");
graph.printGraph();

graph.removeVertex(3);

console.log("\nAfter removal:");
graph.printGraph();

```

```
Before removal:
Vertex:3---> Edges:5 , 4
Vertex:4---> Edges:3
Vertex:5---> Edges:3 , 6
Removing vertex: 3
Checking edges for vertex: 3
Checking edges for vertex: 4
Removing edge from vertex 4 to vertex 3
Checking edges for vertex: 5
Removing edge from vertex 5 to vertex 3
Vertex 3 removed.

After removal:
Vertex:4---> Edges:
Vertex:5---> Edges:6
```
