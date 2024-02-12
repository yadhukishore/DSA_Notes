# Queue

*FIFO manner*


Queue Implementation:-

1. **enqueue(ele)**- Add an element to the Queue.
2. **dequeue()** - Remove the Oldest element from the Queue.
3. **peek()** - get the value of the element at the front of the queue without removing it!
4. **size()** - Get the no.of elements in the queue.
5. **display()** - visualize eles in queue.

```javascript
class Queue{
    constructor(){
        this.items = [];
    }
    enqueue(ele){
        this.items.push(ele);
    }
    dequeue(){
        if(this.items.length === 0){
            return "Empty Queue"
        }else{
            this.items.shift();//remove from front
        }
    }
    peek(){
        if(this.items.length ===0){
            return null;
        }else{
            return this.items[0];
        }
    }
    size(){
        return this.items.length;
    }
    print(){
        console.log(this.items.toString());
    }
}

let q = new Queue();
q.enqueue(90);
q.enqueue(50);
q.enqueue(22);
q.dequeue();//element which entered first(90 is removed)
console.log("element at the front of the queue: ",q.peek());
console.log("Size: ",q.size())
q.print();

```
In this we are using built in methods in JS, so the time complexity will be O(n);
### makeing the Queue Implementation Optimised:-
without using any inbuilt methods:-

forDequeue:-
1. **Store the element at the front of the queue in a variable.**
2. **elements are stored in the items object, and the front variable keeps track of the index of the front element.**
3. **Once the element at the front of the queue is retrieved, it needs to be removed from the queue. This line uses the delete operator to remove the element from the items object.**
4. ** After dequeuing the element, the front index needs to be incremented to point to the next element in the queue. This step ensures that the front index always reflects the index of the front element in the queue after dequeuing an element.**

```javascript
//-enqueue --->rear|||||||||front<----dequeue-

class Queue{
    constructor(){
        this.items = {};
        this.rear = 0;
        this.front = 0;
    }
    enqueue(ele){
        this.items[this.rear]=ele;
        this.rear++;
    }
    dequeue(){
       const dequeEle = this.items[this.front];
       delete this.items[this.front];
       this.front++;
       return dequeEle;
    }
    isEmpty(){
        return this.rear - this .front === 0;
    }
    peek(){
        return this.items[this.front];
    }
    size(){
        return this.rear - this.front;
    }
    print(){
        console.log(this.items);
    }
}

let q = new Queue();
console.log("Is Q empty?: ",q.isEmpty());
q.enqueue(10);
q.enqueue(25);
q.enqueue(30);
q.dequeue();
console.log("First ele in Q: ",q.peek());
q.print();
console.log("Sizee:", q.size())
console.log("Is Q empty?: ",q.isEmpty());
```


## Queue Usage:-
1. **Printers** : when we try to print multiple documents.
2. **CPU task Scheduling**
3. **CallBack queue in JavaScript runtime**
