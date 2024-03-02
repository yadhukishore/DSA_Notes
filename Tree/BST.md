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
