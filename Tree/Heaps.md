# MIN-Heap(iterative)
### insertion to min heap
```javascript
class MinHeap {
    constructor() {
        this.heap = [];
        this.size = 0;
    }

    // Get the parent index of a node
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
    }

    // Get the left child index of a node
    getLeftChildIndex(index) {
        return index * 2 + 1;
    }

    // Get the right child index of a node
    getRightChildIndex(index) {
        return index * 2 + 2;
    }

    hasParent(index){
        return this.getParentIndex(index)>=0;
    }
    hasLeftChild(index){
        return this.getLeftChildIndex(index)<this.size;
    }
    hasRightChild(index){
        return this.getRightChildIndex(index)<this.size;
    }
    swap(index1,index2){
        let tmp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = tmp;
    }
    
    insert(data){
        this.heap[this.size] = data;//insert @ last availabe pos in heap;
        this.size+=1;//inc the size;
        this.heapifyUp();//to check data is in right pos!!!
    }
    heapifyUp(){
        let index = this.size-1;//starting pos;
        while(this.hasParent(index) && this.heap[this.getParentIndex(index)]>this.heap[index]){
            this.swap(this.getParentIndex(index),index);
            index =this.getParentIndex(index);
        }
    }
    
}

// Example usage:
const minHeap = new MinHeap();
minHeap.insert(10);
minHeap.insert(5);
minHeap.insert(15);
minHeap.insert(3);
minHeap.insert(7);

console.log("Min heap:", minHeap.heap); // Output the heap array
```
## Min Heap(Recursive)
```javascript
class MinHeap {
    constructor() {
        this.heap = [];
        this.size = 0;
    }

    // Get the parent index of a node
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
    }

    // Get the left child index of a node
    getLeftChildIndex(index) {
        return index * 2 + 1;
    }

    // Get the right child index of a node
    getRightChildIndex(index) {
        return index * 2 + 2;
    }

    hasParent(index){
        return this.getParentIndex(index)>=0;
    }
    hasLeftChild(index){
        return this.getLeftChildIndex(index)<this.size;
    }
    hasRightChild(index){
        return this.getRightChildIndex(index)<this.size;
    }
    swap(index1,index2){
        let tmp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = tmp;
    }
    //Recursive
    insert(data){
        this.heap[this.size] = data;//insert @ last availabe pos in heap;
        this.size+=1;//inc the size;
        this.heapifyUp(this.size-1);//to check data is in right pos(Pass the index of inserted last data as starting pos)
    }
    heapifyUp(index){
        // let index = this.size-1;//starting pos;
        if(this.hasParent(index) && this.heap[this.getParentIndex(index)]>this.heap[index]){
            this.swap(this.getParentIndex(index),index);
            // index =this.(index);
            this.heapifyUp(this.getParentIndex(index));
        }
    }
    
}

// Example usage:
const minHeap = new MinHeap();
minHeap.insert(10);
minHeap.insert(5);
minHeap.insert(15);
minHeap.insert(3);
minHeap.insert(7);

console.log("Min heap:", minHeap.heap); // Output the heap array

``` 
# Min Heap Remove method
```javascript
class MinHeap {
    constructor() {
        this.heap = [];
        this.size = 0;
    }

    // Get the parent index of a node
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
    }

    // Get the left child index of a node
    getLeftChildIndex(index) {
        return index * 2 + 1;
    }

    // Get the right child index of a node
    getRightChildIndex(index) {
        return index * 2 + 2;
    }

    hasParent(index){
        return this.getParentIndex(index)>=0;
    }
    hasLeftChild(index){
        return this.getLeftChildIndex(index)<this.size;
    }
    hasRightChild(index){
        return this.getRightChildIndex(index)<this.size;
    }
    swap(index1,index2){
        let tmp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = tmp;
    }

    insert(data){
        this.heap[this.size] = data;//insert @ last availabe pos in heap;
        this.size+=1;//inc the size;
        this.heapifyUp(this.size-1);//to check data is in right pos(Pass the index of inserted last data as starting pos)
    }
    heapifyUp(){
        let index = this.size-1;//starting pos;
        while(this.hasParent(index) && this.heap[this.getParentIndex(index)]>this.heap[index]){
            this.swap(this.getParentIndex(index),index);
            index =this.getParentIndex(index);
        }
    }
    removeMin(){
        if(this.size === 0){
            throw new Error("Empty heapp!");
        }
        let data = this.heap[0];
        this.heap[0]=this.heap[this.size-1];
        this.size -=1;
        this.heapifyDown();//check every nodes are in correct Pos!
        return data;
    };
    heapifyDown(){
        let index =0;//start from the root node!
        while(this.getLeftChildIndex(index))//its a CT,So if there is no LeftC,then no Right child also
        {
            let smallerChild=this.getLeftChildIndex(index);
            if(this.hasRightChild(index) && this.heap[this.getRightChildIndex(index)]<this.heap[this.getLeftChildIndex(index)]){
                smallerChild=this.getRightChildIndex(index);
            }
            if(this.heap[index]<this.heap[smallerChild]){
                break;
            }else{
                this.swap(index,smallerChild);
                index=smallerChild;
            }
        }
        
    }
    
}

// Example usage:
const minHeap = new MinHeap();
minHeap.insert(10);
minHeap.insert(5);
minHeap.insert(15);
minHeap.insert(3);
minHeap.insert(7);

console.log("Min heap:", minHeap.heap); // Output the heap array
minHeap.removeMin();
console.log("Min heap After removal:", minHeap.heap);

```

#      MAXHEAP
**Insert Maxheap**
```javascript
class MaxHeap {
    constructor() {
        this.heap = [];
        this.size = 0;
    }

    // Get the parent index of a node
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
    }

    // Get the left child index of a node
    getLeftChildIndex(index) {
        return index * 2 + 1;
    }

    // Get the right child index of a node
    getRightChildIndex(index) {
        return index * 2 + 2;
    }

    hasParent(index) {
        return this.getParentIndex(index) >= 0;
    }

    hasLeftChild(index) {
        return this.getLeftChildIndex(index) < this.size;
    }

    hasRightChild(index) {
        return this.getRightChildIndex(index) < this.size;
    }

    swap(index1, index2) {
        let tmp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = tmp;
    }

    insert(data) {
        this.heap[this.size] = data; // insert at last available position in heap
        this.size += 1; // increment the size
        this.heapifyUp(); // to check if data is in the right position
    }

    heapifyUp() {
        let index = this.size - 1; // starting position
        while (this.hasParent(index) && this.heap[this.getParentIndex(index)] < this.heap[index]) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }
}

// Example usage:
const maxHeap = new MaxHeap();
maxHeap.insert(10);
maxHeap.insert(5);
maxHeap.insert(15);
maxHeap.insert(3);
maxHeap.insert(7);

console.log("Max heap:", maxHeap.heap); // Output the heap array

```

## Remove on Max HeaP

```javascript
class MaxHeap {
    constructor() {
        this.heap = [];
        this.size = 0;
    }

    // Get the parent index of a node
    getParentIndex(index) {
        return Math.floor((index - 1) / 2);
    }

    // Get the left child index of a node
    getLeftChildIndex(index) {
        return index * 2 + 1;
    }

    // Get the right child index of a node
    getRightChildIndex(index) {
        return index * 2 + 2;
    }

    hasParent(index) {
        return this.getParentIndex(index) >= 0;
    }

    hasLeftChild(index) {
        return this.getLeftChildIndex(index) < this.size;
    }

    hasRightChild(index) {
        return this.getRightChildIndex(index) < this.size;
    }

    swap(index1, index2) {
        let tmp = this.heap[index1];
        this.heap[index1] = this.heap[index2];
        this.heap[index2] = tmp;
    }

    insert(data) {
        this.heap[this.size] = data; // insert at last available position in heap
        this.size += 1; // increment the size
        this.heapifyUp(); // to check if data is in the right position
    }

    heapifyUp() {
        let index = this.size - 1; // starting position
        while (this.hasParent(index) && this.heap[this.getParentIndex(index)] < this.heap[index]) {
            this.swap(this.getParentIndex(index), index);
            index = this.getParentIndex(index);
        }
    }

    removeMax() {
        if (this.size === 0) {
            throw new Error("Empty heap!");
        }
        const max = this.heap[0]; // Store the maximum value (root)
        this.heap[0] = this.heap[this.size - 1]; // Replace the root with the last element
        this.size -= 1; // Decrease the size
        this.heapifyDown(); // Restore the max-heap property
        return max; // Return the removed maximum value
    }

    heapifyDown() {
        let index = 0; // Start from the root node
        while (this.hasLeftChild(index)) {
            let maxChildIndex = this.getLeftChildIndex(index);
            if (this.hasRightChild(index) && this.heap[this.getRightChildIndex(index)] > this.heap[maxChildIndex]) {
                maxChildIndex = this.getRightChildIndex(index);
            }
            if (this.heap[index] > this.heap[maxChildIndex]) {
                break; // If the current node is greater than its children, heap property is satisfied
            } else {
                this.swap(index, maxChildIndex); // Otherwise, swap with the maximum child
                index = maxChildIndex; // Update the index for next iteration
            }
        }
    }
}

// Example usage:
const maxHeap = new MaxHeap();
maxHeap.insert(10);
maxHeap.insert(5);
maxHeap.insert(15);
maxHeap.insert(3);
maxHeap.insert(7);

console.log("Max heap:", maxHeap.heap); // Output the heap array
console.log("Removing max value:", maxHeap.removeMax()); // Output the removed maximum value
console.log("Max heap after removal:", maxHeap.heap); // Output the heap array after removal

```

## Explanation of heapy up and down

In the context of a heap data structure, "heapify up" and "heapify down" refer to two different processes used to maintain the heap property during insertions or deletions.

- **Heapify Up**: This process is used when a new element is added to the heap and needs to be placed in its correct position to maintain the heap property. Starting from the newly added element, it compares the element with its parent. If the element is smaller (in a min-heap) or larger (in a max-heap) than its parent, the element is swapped with its parent. This process continues up the heap until the element is in its correct position or the root of the heap is reached. The code snippet for heapify up is provided in Source 1, where it iterates through each element, comparing it with its parent and swapping them if necessary until the heap property is restored.

- **Heapify Down**: This process is used to restore the heap property after an element has been removed from the heap or after a new element has been added and placed at the root. Starting from the root, it compares the root with its children. If the root is smaller (in a min-heap) or larger (in a max-heap) than either of its children, the root is swapped with the larger (in a min-heap) or smaller (in a max-heap) child. This process continues down the heap until the element is in its correct position or a leaf node is reached. The code snippet for heapify down is also provided in Source 1, where it iterates from the root downwards, ensuring that the heap property is maintained at each step.

Heapify up is typically used when adding a new element to the heap, ensuring that the new element is placed in its correct position without disrupting the heap property. Heapify down is used after removing the root element or after adding a new element at the root, ensuring that the heap property is maintained throughout the heap [1][2].
