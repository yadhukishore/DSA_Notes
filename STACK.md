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

*simply:-*

(Each if statement checks if the current character c is an opening bracket ((, [, or {), and if so, it pushes the corresponding closing bracket onto the stack. Otherwise, if c is a closing bracket, it compares it with the top of the stack to see if they match. If they don't match, it returns false. Finally, after iterating through all characters in the string, it checks if the stack is empty to ensure all opening brackets have been matched with closing brackets. If the stack is empty, it returns true, indicating a valid sequence of brackets.)

Here's the JavaScript implementation of the algorithm:

```javascript
function validParantesis(s){
const stack = [];
    
    for (let i = 0; i < s.length; i++) {
        let c = s.charAt(i);
        if (c === '(') {
            stack.push(')');
        } else if (c === '[') {
            stack.push(']');
        } else if (c === '{') {
            stack.push('}');
        } else {
            if (c !== stack.pop()) {
                return false;
            }
        }
    }
    
    return stack.length === 0;
};
console.log(validParantesis("(())"))
```

This algorithm has a time complexity of O(n), where n is the length of the input string `s`. It efficiently validates whether the string contains valid pairs of parentheses, square brackets, and curly braces.




## 151. Reverse Words in a String
Given an input string s, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in s will be separated by at least one space.

Return a string of the words in reverse order concatenated by a single space.

*Note* that s may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

Example 1:

Input: s = "the sky is blue"
Output: "blue is sky the"
Example 2:

Input: s = "  hello world  "
Output: "world hello"
Explanation: Your reversed string should not contain leading or trailing spaces.
Example 3:

Input: s = "a good   example"
Output: "example good a"
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.

### Algo:-
1. **split the stings on the basis of whitespace**
2. **push all vals to stack**
3. **Pop all the values in the stack to a new string variable**
4. **return that varible with `trim()` method which removes whitespace from both sides of a string.**


```javascript
 function reverseWords(s){
     const splitS = s.split(" ");
     const stack =[];
     for(let val of splitS){
         stack.push(val);
     }
     
     let finalS="";
     while(stack.length){
         const curr = stack.pop();
         if(curr){
             finalS += " "+curr;       
             }
     }
     return finalS.trim();
 }
```

## Next Greater Element: Find the next greater element for every element in an array. This problem can be solved using a stack to keep track of elements and their indices.

To solve the Next Greater Element (NGE) problem using a stack in JavaScript, you can follow these steps:

1. Initialize an empty stack and an array `nextGreater` of the same length as the input array to store the NGE for each element.
2. Iterate through the input array from right to left.
3. For each element, while the stack is not empty and the top element of the stack is less than or equal to the current element, pop the stack.
4. If the stack is empty after the above step, it means there is no greater element to the right of the current element, so set `nextGreater[i]` to `-1`.
5. If the stack is not empty, the top element of the stack is the next greater element to the right of the current element, so set `nextGreater[i]` to the top element of the stack.
6. Push the current element onto the stack.
7. After iterating through the input array, the `nextGreater` array will contain the NGE for each element.

Here's the JavaScript code implementing the above algorithm:

```javascript
function nextGreaterElement(arr) {
    let stack = [];
    let nextGreater = new Array(arr.length).fill(-1);
    
    for (let i = arr.length -  1; i >=  0; i--) {
        while (stack.length >  0 && stack[stack.length -  1] <= arr[i]) {
            stack.pop();
        }
        
        if (stack.length ===  0) {
            nextGreater[i] = -1;
        } else {
            nextGreater[i] = stack[stack.length -  1];
        }
        
        stack.push(arr[i]);
    }
    
    return nextGreater;
}
```

This function uses a stack to keep track of the elements that have been processed but do not yet have a next greater element. When it encounters an element that is greater than the top of the stack, it pops elements from the stack and assigns the current element as the next greater element to them.

The time complexity of this solution is O(n), where n is the length of the array, because each element is pushed and popped from the stack exactly once. The space complexity is O(n) for the stack and the `nextGreater` array.
