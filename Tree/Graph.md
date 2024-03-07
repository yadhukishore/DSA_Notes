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
