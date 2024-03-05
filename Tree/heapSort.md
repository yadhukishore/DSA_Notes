# HeapSort
### putting the removed root to the array **Using Maxheap**
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
function heapSort(arr){
    const maxHeap = new MaxHeap();
    for(let i=0 ; i<arr.length;i++){
        maxHeap.insert(arr[i]);
    }
    const sortedResult=[];
    while (maxHeap.size>0){
        sortedResult.unshift(maxHeap.removeMax());
    }
    return sortedResult;
}

// Example usage:
const array = [10, 5, 15, 3, 7];
console.log("Original array:", array);
const sortedArray = heapSort(array);
console.log("Sorted array:", sortedArray);

```

The line `sortedArray.unshift(maxHeap.removeMax());` performs two operations:

1. `maxHeap.removeMax()`: This method removes the maximum element from the max heap (`maxHeap`) and returns that element. It effectively removes the root node of the heap, which is the maximum element in the heap.

2. `sortedArray.unshift(...)`: This method adds the element returned by `maxHeap.removeMax()` to the beginning of the `sortedArray`. `unshift()` is a method in JavaScript arrays that adds one or more elements to the beginning of an array and returns the new length of the array.

### if we are using minHeap, we need to push it to the sortedResult;

```javascript
function heapSort(arr) {
    const minHeap = new MinHeap();
    for (let i = 0; i < arr.length; i++) {
        minHeap.insert(arr[i]);
    }
    const sortedArray = [];
    while (minHeap.size > 0) {
        sortedArray.push(minHeap.removeMin());
    }
    return sortedArray;
}
```
