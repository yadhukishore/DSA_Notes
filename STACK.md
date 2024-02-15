## Stack Array:-

*LIFO MANNER*

```javascript
class Stack{
    constructor(){
        this.stack=[];
        this.top=-1;
    }
    
    push(ele){
        this.top++;
        this.stack.push(ele);
    }
    pop(){
        if(this.top === -1){
            console.log("Stack UnderFlow!");
            return;
        }else{
        this.top--;
        return this.stack.pop();
        }
            
        }
        peek(){       //to find the top element in the stack?
          if(this.top === -1){
               console.log("Stack is empty!");
            return;
          }else{
              return this.stack[this.top];
          }
        }
        size(){
            return this.top + 1;
        }
        clear(){
            this.stack = [];
            this.top = -1;
        }
 printStack(){
             if(this.top ===-1){
            console.log("Empty")
        }else{
            for(let i=this.top ; i>=0 ; i--){
                console.log(this.stack[i]);
            }
        }
    }

}



let stk = new Stack();
stk.push(5);
stk.push(10);
stk.push(25);
stk.pop();
stk.push(100);
console.log("Top element of stack:", stk.peek()); 
console.log("Size of stack: ",stk.size());

console.log(stk.stack)//Displays the current stack

stk.clear(); // Clears the stack

console.log(stk.stack);//Displays the current stack
```
1. **peek(): Returns the top element of the stack without removing it.**
2. **isEmpty(): Checks if the stack is empty and returns a boolean value.**
3. **size(): Returns the number of elements in the stack.**
4. **clear(): Clears the stack by resetting the stack array and top pointer.**

## Stack LinkedList

In this implementation:

1. **We define a Node class to represent each element of the linked list.**
2. **The Stack class maintains a reference to the top element of the stack (top) and keeps track of the size of the stack (size).**
3. **The push() method adds a new node containing the data to the top of the stack.**
4. **The pop() method removes and returns the top element from the stack.**
5. **The peek() method returns the data of the top element without removing it.**
6. **The isEmpty() method checks if the stack is empty.**
7. **The getSize() method returns the size of the stack.**

```javascript
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}

class Stack{
    constructor(){
        this.top = null;
        this.size =0;
    }
    
    push(data){
        let newNode = new Node(data);
        newNode.next = this.top;
        this.top = newNode;
        this.size++;
    }
    pop(){
        if(!this.top){
             console.log("Stack Underflow!");
            return;
        }
        let popped = this.top;
        this.top = this.top.next;
        this.size--;
        return popped.data;
    }
    peek(){
          if(!this.top){
             console.log("Stack Underflow!");
            return;
        }
        else{
            return this.top.data;
        }
    }
      getSize() {
        return this.size;
    }
    display(){
        if(!this.top){
            console.log("Empty Stack!");
            return;
        }else{
            let curr = this.top;
            while(curr){
                console.log(curr.data);
                curr = curr.next;
            }
        }
    }
}

let stk = new Stack();
stk.push(11);
stk.push(22);
stk.push(33);
stk.pop();
console.log("Top element of stack:", stk.peek());
console.log("Size of stack:", stk.getSize()); 
stk.display();
```

**In a basic implementation of a stack using a linked list, the tail pointer is not necessary. This is because we typically only need to access and manipulate the top of the stack, which is represented by the top pointer.**

**So, while the tail pointer is not strictly necessary for a basic stack implementation, its inclusion depends on the specific requirements and functionalities of the stack you are implementing.**

## Stack Usage
1. **Browser History Tracking**
2.  **Undo operation when Typing**
3.  **Expression Conversions(*infix to postfix*)**
4.  **Call Stack in JS**



# LeetCode
## Valid Parantesis:-

Example 1:

Input: s = "()"
Output: true
Example 2:

Input: s = "()[]{}"
Output: true
Example 3:

Input: s = "(]"
Output: false

Certainly! Here's a simple algorithm to determine whether a string containing only parentheses, square brackets, and curly braces is valid:

1. **Initialize an empty stack** to store opening parentheses, square brackets, and curly braces encountered while traversing the string.

2. **Iterate through the string** character by character:
   - For each character `c` in the string:
     - If `c` is an opening parenthesis, square bracket, or curly brace (i.e., `'('`, `'['`, or `'{'`), push its corresponding closing parenthesis, square bracket, or curly brace onto the stack.
     - If `c` is a closing parenthesis, square bracket, or curly brace (i.e., `')'`, `']'`, or `'}'`):
       - Pop the top element from the stack and compare it with `c`.
         - If they are not the same, return `false` as the string is invalid.
         - If they are the same, continue iterating through the string.

3. **After iterating through the entire string**, check if the stack is empty:
   - If the stack is empty, return `true` as all opening parentheses, square brackets, and curly braces have been matched with their corresponding closing characters.
   - If the stack is not empty, return `false` as there are unmatched opening characters in the string.

Here's the JavaScript implementation of the algorithm:

```javascript
var isValid = function(s) {
    const stack = [];
    
    for (let i = 0; i < s.length; i++) {
        let c = s.charAt(i);
        switch (c) {
            case '(': stack.push(')');
                break;
            case '[': stack.push(']');
                break;
            case '{': stack.push('}');
                break;
            default:
                if (c !== stack.pop()) {
                    return false;
                }
        }
    }
    
    return stack.length === 0;
};
```

This algorithm has a time complexity of O(n), where n is the length of the input string `s`. It efficiently validates whether the string contains valid pairs of parentheses, square brackets, and curly braces.


