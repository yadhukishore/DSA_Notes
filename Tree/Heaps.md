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
