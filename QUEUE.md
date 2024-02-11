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



## Queue Usage:-
1. **Printers** : when we try to print multiple documents.
2. **CPU task Scheduling**
3. **CallBack queue in JavaScript runtime**
