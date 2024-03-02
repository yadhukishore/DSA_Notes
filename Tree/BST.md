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
