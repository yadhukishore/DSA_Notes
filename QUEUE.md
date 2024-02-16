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
        this.items.push(ele);//adding at the end
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
//<--Front(dequeue)-- |||||| <---Rear(enqueue)---

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

## Types of Queues:-
- **Priority Queue**
- **Doubley ended Q**
- **Circular Queue**

# (Leet)225. Implement Stack using Queues

Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).

Implement the MyStack class:

void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.


```javascript
//225. Implement Stack using Queues




var MyStack = function() {
    this.q1=[];
    this.q2=[];
};

/** 
 * @param {number} x
 * @return {void}
 */
MyStack.prototype.push = function(x) {
    while(this.q1.length !==0){
        this.q2.push(this.q1.shift());
    }
    this.q1.push(x);
    while(this.q2.length !==0){
        this.q1.push(this.q2.shift());
    }
};

/**
 * @return {number}
 */
MyStack.prototype.pop = function() {
   return this.q1.shift();
};

/**
 * @return {number}
 */
MyStack.prototype.top = function() {
    return this.q1[0];
};

/**
 * @return {boolean}
 */
MyStack.prototype.empty = function() {
  return this.q1.length ===0;  
};

/** 
 * Your MyStack object will be instantiated and called as such:
 * var obj = new MyStack()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.top()
 * var param_4 = obj.empty()
 */
```

# Leet(232). Implement Queue using Stacks
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).

Implement the MyQueue class:

void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise.

```javascript
/**
 * Initialize your data structure here.
 */
var MyQueue = function() {
	this.stack1 = []
	this.stack2 = []
};

/**
 * Push element x to the back of queue. 
 * @param {number} x
 * @return {void}
 */
MyQueue.prototype.push = function(x) {
	this.stack1.push(x)
};

/**
 * Removes the element from in front of queue and returns that element.
 * @return {number}
 */
MyQueue.prototype.pop = function() {
	while(this.stack1.length !== 0){
		this.stack2.push(this.stack1.pop())
	}

	var pop = this.stack2.pop()

	while(this.stack2.length !== 0){
		this.stack1.push(this.stack2.pop())
	}

	return pop
};

/**
 * Get the front element.
 * @return {number}
 */
MyQueue.prototype.peek = function() {
	while(this.stack1.length !== 0){
		this.stack2.push(this.stack1.pop())
	}

	var pop = this.stack2.pop()
	this.stack2.push(pop)
	while(this.stack2.length !== 0){
		this.stack1.push(this.stack2.pop())
	}

	return pop
};

/**
 * Returns whether the queue is empty.
 * @return {boolean}
 */
MyQueue.prototype.empty = function() {
	return this.stack1.length === 0 ? true:false
};

/** 
 * Your MyQueue object will be instantiated and called as such:
 * var obj = new MyQueue()
 * obj.push(x)
 * var param_2 = obj.pop()
 * var param_3 = obj.peek()
 * var param_4 = obj.empty()
 */
```

## LinkedList Queue:-
```javascript
//<--Front(dequeue)---|||||| <---Rear(enqueue)---

class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}
class Queue{
    constructor(){
        this.rear=null;// Pointer to the rear of the queue
        this.front = null;// // Pointer to the front of the queue
        this.size = 0;
        
    }
    
    enqueue(data){
        let newNode = new Node(data);
        if(this.isEmpty()){
            this.front = newNode;
        }else{
            this.rear.next = newNode;
        }
        this.rear = newNode;
        this.size++;
        
    }
    dequeue(){
        if(this.isEmpty()){
            console.log("Q is empty;")
        }
        let dequeuedItem = this.front.data;
        this.front = this.front.next;
        if(!this.front){
            this.rear = null;
        }
        this.size--;
        return dequeuedItem;
    }
      isEmpty() {
        return this.size === 0;
    }
    getSize(){
        return this.size;
    }
    display(){
        if(this.isEmpty()){
            console.log("Queue is Empty");
            return;
        }
        let curr = this.front;
        while(curr){
            console.log(curr.data);
            curr = curr.next;
        }
    }
    
  
}
  let q = new Queue();
  q.enqueue(1);
  q.enqueue(2);
  q.enqueue(3);
  q.dequeue();
  q.display();
```
