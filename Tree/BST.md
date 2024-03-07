# Binary Search tree
### insert & Search method:

```javascript
class Node {
    constructor(value){
    this.value=value;
    this.left=null;
    this.right=null;
    }
}
class BST{
    constructor(){
        this.root=null;
    }
    isEmpty(){
        return this.root===null;
    }
    insert(value){
        const newNode = new Node();
        if(this.isEmpty()){
            this.root = newNode;
        }
        else{
            this.insertNode(this.root,newNode)
        }
    }
    insertNode(root,newNode){
        if(newNode.value < root.value){
            if(root.left === null){
                root.left = newNode;
            }
            else{
                this.insertNode(root.left,newNode);
            }
        }else{
            if(root.right === null){
                root.right = newNode;
            } else {
                this.insertNode(root.right,newNode);
            }
        }
    }
    search(root, value){
        if(!root){
            return false;
        } else {
            if(root.value === value){
                return true;
            } else if(value < root.value){
                return this.search(root.left, value);
            } else{
                return this.search(root.right, value);
            }
        }
    }
}
const bst = new BST();
console.log('Empty?: ',bst.isEmpty());

bst.insert(10);
bst.insert(20);
bst.insert(30);
console.log(bst.search(bst.root,20));


```

## Tree travesal (postorder, preorder, in order)

```javascript
class Node {
    constructor(value){
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor(){
        this.root = null;
    }

    isEmpty(){
        return this.root === null;
    }

    insert(value){
        const newNode = new Node(value);
        if(this.isEmpty()){
            this.root = newNode;
        }
        else{
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode){
        if(newNode.value < root.value){
            if(root.left === null){
                root.left = newNode;
            }
            else{
                this.insertNode(root.left, newNode);
            }
        }else{
            if(root.right === null){
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }

    search(root, value){
        if(!root){
            return false;
        } else {
            if(root.value === value){
                return true;
            } else if(value < root.value){
                return this.search(root.left, value);
            } else{
                return this.search(root.right, value);
            }
        }
    }

    inorderTraversal(node){
        if(node !== null){
            this.inorderTraversal(node.left);
            console.log(node.value);
            this.inorderTraversal(node.right);
        }
    }
    preorderTraversal(node){
        if(node !==null){
            console.log(node.value);
            this.preorderTraversal(node.left);
            this.preorderTraversal(node.right);
        }
    }
    postorderTraversal(node){
        if(node !==null){
            this.postorderTraversal(node.left);
            this.postorderTraversal(node.right);
            console.log(node.value);
        }
    }

}

const bst = new BST();
console.log('Empty?: ', bst.isEmpty());

bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

console.log("Inorder Traversal:");
bst.inorderTraversal(bst.root);
console.log("preorder Traversal:");
bst.preorderTraversal(bst.root);
console.log("postorder Traversal:");
bst.postorderTraversal(bst.root);

console.log("Is 5 in the BST?", bst.search(bst.root, 5)); // true
console.log("Search 15?:",bst.search(bst.root,15));//true

```

## Delete node 
### Check Audio in whatsapp
```javascript
class Node {
    constructor(value){
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor(){
        this.root = null;
    }

    isEmpty(){
        return this.root === null;
    }

    insert(value){
        const newNode = new Node(value);
        if(this.isEmpty()){
            this.root = newNode;
        } else {
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode){
        if(newNode.value < root.value){
            if(root.left === null){
                root.left = newNode;
            } else {
                this.insertNode(root.left, newNode);
            }
        } else {
            if(root.right === null){
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }

    inorderTraversal(node){
        if(node !== null){
            this.inorderTraversal(node.left);
            console.log(node.value);
            this.inorderTraversal(node.right);
        }
    }

delete(value){
    this.root = this.deleteNode(this.root, value);
}
deleteNode(root,value){
    if(root === null){
        return root;
    } 
    if(value<root.value){
        root.left = this.deleteNode(root.left,value);
    }else if(value>root.value){
        root.right = this.deleteNode(root.right,value);
    }else{
          // Node with only one child or no child
          if(root.left===null){
              return root.right;
          }else if(root.right === null){
              return root.left;
          }
          
// Node with two children: Get the inorder successor (smallest in the right subtree)
root.value = this.minValue(root.right);
root.right = this.deleteNode(root.right, root.value);



    }
    return root;
}

minValue(node){
    let minVal = node.value;
    while(node.left !== null){
        minVal = node.left.value;
        node = node.left;
    }
    return minVal;
}

}

// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

console.log("Before deletion:");
bst.inorderTraversal(bst.root);

bst.delete(10);

console.log("\nAfter deletion:");
bst.inorderTraversal(bst.root);
```

## To find the closest Node

```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    insert(value) {
        const newNode = new Node(value);
        if (this.root === null) {
            this.root = newNode;
        } else {
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode) {
        if (newNode.value < root.value) {
            if (root.left === null) {
                root.left = newNode;
            } else {
                this.insertNode(root.left, newNode);
            }
        } else {
            if (root.right === null) {
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }
 findClosest(target){
     return this.findClosestValueHelper(this.root,target,Infinity);
 }   
 findClosestValueHelper(node,t,closest){
     if(node === null){
         return closest;
     }
     if(Math.abs(node.value-t)<Math.abs(closest-t)){
         closest = node.value;
     }
     if(t<node.value){
         return this.findClosestValueHelper(node.left,t,closest);
     }else if(t>node.value){
         return this.findClosestValueHelper(node.right,t,closest);
     } else {
         return closest;
     }
 }
}


// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

const target = 226;
const closestValue = bst.findClosest(target);
console.log(`Closest value to ${target} is ${closestValue}`);
```

## Validate its BST or not

```javascript
class Node {
    constructor(value){
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST{
    constructor(){
        this.root = null;
    }
    isEmpty(){
        return this.root === null;
    }
    insert(value){
        const newNode = new Node(value); // Corrected: Pass value to Node constructor
        if(this.isEmpty()){
            this.root = newNode;
        }
        else{
            this.insertNode(this.root, newNode);
        }
    }
    insertNode(root, newNode){
        if(newNode.value < root.value){
            if(root.left === null){
                root.left = newNode;
            }
            else{
                this.insertNode(root.left, newNode);
            }
        }else{
            if(root.right === null){
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }
    search(root, value){
        if(!root){
            return false;
        } else {
            if(root.value === value){
                return true;
            } else if(value < root.value){
                return this.search(root.left, value);
            } else{
                return this.search(root.right, value);
            }
        }
    }

    isBST(node, min = null, max = null) {
        if (node === null) {
            return true; // An empty tree is a BST
        }

        if (min !== null && node.value <= min) {
            return false; // The node's value is not greater than the minimum
        }

        if (max !== null && node.value >= max) {
            return false; // The node's value is not less than the maximum
        }

        // Check the left and right subtrees with updated min and max values
        return this.isBST(node.left, min, node.value) && this.isBST(node.right, node.value, max);
    }
}

const bst = new BST();
console.log('Empty?: ', bst.isEmpty());

bst.insert(10);
bst.insert(20);
bst.insert(30);
console.log(bst.search(bst.root, 20));

// Validate if the tree is a BST
console.log('Is BST?: ', bst.isBST(bst.root)); // Pass the root node to isBST method

```

## Height of the tree

```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    isEmpty() {
        return this.root === null;
    }

    insert(value) {
        const newNode = new Node(value);
        if (this.isEmpty()) {
            this.root = newNode;
        } else {
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode) {
        if (newNode.value < root.value) {
            if (root.left === null) {
                root.left = newNode;
            } else {
                this.insertNode(root.left, newNode);
            }
        } else {
            if (root.right === null) {
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }

    getHeight(node = this.root) {
        if (node === null) {
            return -1; // Height of an empty tree is -1
        }

        // Recursively compute the height of the left and right subtrees
        const leftHeight = this.getHeight(node.left);
        const rightHeight = this.getHeight(node.right);

        // Return the maximum height among the left and right subtrees, plus 1 for the current node
        return Math.max(leftHeight, rightHeight) + 1;
    }
}

// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

console.log('Height of the BST:', bst.getHeight());
```
### Height of  node:-
```javascript
  getNodeHeight(target, node = this.root) {
        if (node === null) {
            return -1; // Height of a non-existent node is -1
        }

        if (node.value === target) {
            return this.getHeight(node); // Return height of the current node
        }

        // Recursively search in the left and right subtrees
        const leftHeight = this.getNodeHeight(target, node.left);
        const rightHeight = this.getNodeHeight(target, node.right);

        // Return the maximum height among the left and right subtrees
        return Math.max(leftHeight, rightHeight);
    }

    getHeight(node) {
        if (node === null) {
            return -1; // Height of an empty tree is -1
        }

        // Recursively compute the height of the left and right subtrees
        const leftHeight = this.getHeight(node.left);
        const rightHeight = this.getHeight(node.right);

        // Return the maximum height among the left and right subtrees, plus 1 for the current node
        return Math.max(leftHeight, rightHeight) + 1;
    }
}
```
## Depth of the node in bst
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    isEmpty() {
        return this.root === null;
    }

    insert(value) {
        const newNode = new Node(value);
        if (this.isEmpty()) {
            this.root = newNode;
        } else {
            this.insertNode(this.root, newNode);
        }
    }

    insertNode(root, newNode) {
        if (newNode.value < root.value) {
            if (root.left === null) {
                root.left = newNode;
            } else {
                this.insertNode(root.left, newNode);
            }
        } else {
            if (root.right === null) {
                root.right = newNode;
            } else {
                this.insertNode(root.right, newNode);
            }
        }
    }

    getNodeDepth(target, node = this.root, depth = 0) {
        if (node === null) {
            return -1; // Target node not found, return -1
        }

        if (node.value === target) {
            return depth; // Found the target node, return the current depth
        }

        // Recursively search in the left and right subtrees
        const leftDepth = this.getNodeDepth(target, node.left, depth + 1);
        const rightDepth = this.getNodeDepth(target, node.right, depth + 1);

        // Return the maximum depth among the left and right subtrees
        return Math.max(leftDepth, rightDepth);
    }
}

// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

const targetNodeValue = 7;
console.log(`Depth of node with value ${targetNodeValue}:`, bst.getNodeDepth(targetNodeValue));

```

# Find the Minimum and Maximum Elements?

```javascript

class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    // Insert a new node into the BST
    insert(value) {
        if (!this.root) {
            this.root = new Node(value);
            return;
        }

        let currentNode = this.root;
        while (true) {
            if (value < currentNode.value) {
                if (!currentNode.left) {
                    currentNode.left = new Node(value);
                    return;
                }
                currentNode = currentNode.left;
            } else {
                if (!currentNode.right) {
                    currentNode.right = new Node(value);
                    return;
                }
                currentNode = currentNode.right;
            }
        }
    }

    // Find the minimum value in the BST
    findMin() {
        if (!this.root) {
            return null;
        }
        let currentNode = this.root;
        while (currentNode.left) {
            currentNode = currentNode.left;
        }
        return currentNode.value;
    }

    // Find the maximum value in the BST
    findMax() {
        if (!this.root) {
            return null;
        }
        let currentNode = this.root;
        while (currentNode.right) {
            currentNode = currentNode.right;
        }
        return currentNode.value;
    }
}

// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

console.log("Minimum element:", bst.findMin()); // Output: 3
console.log("Maximum element:", bst.findMax()); // Output: 15

```

# Count the Number of Nodes?

```javascript

class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    // Other methods like insert, search, etc. go here...

    // Function to count the number of nodes in the BST
    countNodes(node = this.root) {
        if (node === null) {
            return 0; // Base case: if the node is null, return 0
        }
        // Recursively count nodes in the left and right subtrees
        return 1 + this.countNodes(node.left) + this.countNodes(node.right);
    }
}

// Example usage:
const bst = new BST();
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);

console.log("Number of nodes:", bst.countNodes()); // Output: 5

```
**The total count is the sum of 1 (for the current node) and the counts of nodes in the left and right subtrees.**
### if i need tofind sum of all node values return `Change 1 to node value`
```
  return node.value+this.countNodes(node.left)+this.countNodes(node.right);
```
# ----Balancing Factor-----

In a binary search tree (BST), the balancing factor is a measure of how balanced the tree is. It's typically defined as the difference in height between the left and right subtrees of a node.

The balancing factor for a node can be calculated as follows:

Balancing Factor (BF) = Height of the left subtree - Height of the right subtree

A balanced tree has a balancing factor of 0, meaning that the heights of its left and right subtrees are equal (or differ by at most 1). If the balancing factor of a node is negative, it indicates that the right subtree is taller, and if it's positive, it indicates that the left subtree is taller.

Here's an implementation of a function to calculate the balancing factor of a node in a BST:

```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.left = null;
        this.right = null;
    }
}

class BST {
    constructor() {
        this.root = null;
    }

    // Other methods like insert, search, etc. go here...

    // Function to calculate the height of a node
    height(node) {
        if (node === null) {
            return 0; // Base case: if the node is null, return 0
        }
        // Recursively calculate the height of the left and right subtrees
        const leftHeight = this.height(node.left);
        const rightHeight = this.height(node.right);
        // Height of the node is the maximum height of its subtrees plus 1
        return Math.max(leftHeight, rightHeight) + 1;
    }

    // Function to calculate the balancing factor of a node
    balancingFactor(node) {
        if (node === null) {
            return 0; // Base case: if the node is null, balancing factor is 0
        }
        // Calculate the height of the left and right subtrees
        const leftHeight = this.height(node.left);
        const rightHeight = this.height(node.right);
        // Balancing factor is the difference in heights of the left and right subtrees
        return leftHeight - rightHeight;
    }
}

// Example usage:
const bst = new BST();
// Insert nodes into the BST
bst.insert(10);
bst.insert(5);
bst.insert(15);
bst.insert(3);
bst.insert(7);
// Calculate the balancing factor of the root node
console.log("Balancing factor of the root node:", bst.balancingFactor(bst.root));
```

In this implementation:

- The `height()` method calculates the height of a node in the tree recursively.
- The `balancingFactor()` method calculates the balancing factor of a node by subtracting the height of the right subtree from the height of the left subtree.
- You can call the `balancingFactor()` method for any node in the BST to determine its balancing factor.
