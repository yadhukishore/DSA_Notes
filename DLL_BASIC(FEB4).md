# Doubly LinkedList Basics

```javascript
class Node{
    constructor(data){
        this.data=data;
        this.next=null;
        this.prev=null;
    }
}
class LinkedList{
    constructor(){
        this.head=null;
        this.tail=null;
        this.size=0;
    }
    add(data){
    const newNode = new Node(data);
    if(this.head === null){
        this.head = newNode;
        this.tail = newNode;
    }
    else{
        newNode.next = this.head;
        this.head.prev = newNode;
        this.head = newNode;
    }this.size++;
}

append(data){
    const newNode = new Node(data);
    if(this.head === null){
        this.head = newNode;
        this.tail = newNode;
    }
    else{
        newNode.prev = this.tail;
        this.tail.next = newNode;
        this.tail = newNode;
    }
}
removeFrom(pos){
    if(pos<0 || pos>=this.size){
        return null;
    }
    let removedNode;
    if(pos === 0){
        removedNode = this.head;
        this.head = this.head.next;
        if(this.head){
            this.head.prev=null;
        }
        else{
            this.tail=null;
        }
    }else if(pos === this.size-1){
        removedNode = this.tail;
        this.tail = this.tail.prev;
        this.tail.next=null;
    }else{
         // Removing a node in the middle
        let curr = this.head;
        for (let i=0;i<pos;i++){
            curr = curr.next;
        }
        removedNode=curr;
        curr.prev.next = curr.next;
        curr.next.prev = curr.prev;
    }
    this.size--;
    return removedNode;
}

insert(data,pos){
    if(pos<0 || pos>this.size){
        return null;
    }
    if(pos === 0){
        this.add(data);
    }else if(pos === this.size){
        this.append(data);
    }else{
        const newNode = new Node(data);
        let curr = this.head;
        for(let i=0;i<pos;i++){
            curr = curr.next;
        }
        newNode.prev =curr.prev;
        newNode.next = curr;
        curr.prev.next = newNode;
        curr.prev = newNode;
        this.size++;
    }
}

display(){
    if(this.head===null){
        return null;
    }
    else{
        let curr = this.head;
        while(curr){
            console.log(curr.data);
            curr = curr.next;
        }
    }
}

}
const list = new LinkedList();
console.log("Size: ",list.size);
// list.add(10);
// list.add(30);
// list.append(100);
// list.append(300);
// list.add(400);
// list.removeFrom(2)
list.insert(10,0)
list.insert(1,0);
list.insert(20,1)
list.insert(50,2);
list.removeFrom(3)
list.display();
console.log("Size: ",list.size);

```
