# Complete SLinkedList
## SLL

```javascript
class Node{
    constructor (data){
        this.data=data;
        this.next=null;
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
        }else{
            newNode.next = this.head;
            this.head=newNode;
        }
        this.size++;
    }
    
    append(data){
        const newNode = new Node(data);
         if(this.head === null){
            this.head = newNode;
            this.tail =newNode;
        }
        else{
            this.tail.next = newNode;
            this.tail = newNode;
        }
        this.size++;
    }
    
    insert(data,pos){
        if(pos<0 || pos>this.size){
            return console.log("POS_Invalid");
        }
        if(pos === 0){
            this.add(data);
        }else if(pos === this.size){
            this.append(data);
        }
        else{
            const newNode = new Node(data);
            let prev = this.head;
            for(let i=0 ; i<pos-1 ; i++){
                prev = prev.next;
            }
            newNode.next = prev.next;
            prev.next=newNode;
            this.size++;
        }
    }
    
    insertAfter(dataToFind,newData){
        const newNode = new Node(newData);
        if(this.head===null){
             console.log("List is empty.");
            return;
        }
        let curr = this.head;
        while(curr){
            if(curr.data === dataToFind){
                newNode.next=curr.next;
                curr.next =newNode;
                if(newNode.next === null){
                    this.tail = newNode;
                }
                this.size++
            }
            curr = curr.next;
        }
    }
    insertBefore(dataToFind,newData){
    const newNode = new Node(newData);
        if(this.head===null){
             console.log("List is empty.");
            return;
        }
        let curr =this.head;
        while(curr.next){
            if(curr.next.data === dataToFind){
                newNode.next = curr.next;
                curr.next = newNode;
                this.size++;
                return;
            }
            curr =curr.next;
        }
        console.log(`${dataToFind} is not Found`)
    }
    removePos(pos){
        if(pos<0 || pos>this.size){
            console.log("Invalid Pos");
            return null;
        }
        let removedNode;
        if(pos===0){
            removedNode=this.head;
            this.head = this.head.next;;
            if(!this.head){
                this.tail = null
            }
        }else{
            let prev  = this.head;
            for(let i = 0; i<pos-1 ; i++){
                prev = prev.next;
            }
            removedNode = prev.next;
            prev.next = removedNode.next;
            if(!removedNode.next){
                this.tail=prev;
            }
        }
        this.size--;
        return removedNode.value
    }
    removeData(data){
        if(this.head===null){
            return null;
        }
        let removedNode;
        if(this.head.data === data){
            removedNode = this.head;
            this.head=removedNode.next;
            this.size--;
        }else{
            let prev = this.head;
            while(prev.next && prev.next.data !== data){
                prev = prev.next;
            }
            if(prev.next){
                removedNode = prev.next;
                prev.next= removedNode.next;
                if(removedNode.next===null){
                    this.tail = prev;
                }
                this.size--;
            }
        }
    }
    
        removeDuplicates(){
        let curr = this.head;
        while(curr && curr.next){
            if(curr.data === curr.next.data){
                curr.next = curr.next.next;
            }else{
                curr = curr.next;
            }
        }
    }
    
    reverse(){
         
        let prev =null;
        let curr = this.head;
        while(curr){
            let next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        this.head=prev;
        let temp = this.head;
        while(temp.next!==null){
            temp = temp.next;
        }
        this.tail = temp;
    }
    
    display(){
        if(this.head===null){
            console.log("Empty")
            return ; 
        }
        let curr = this.head;
        while(curr){
            console.log(curr.data);
            curr = curr.next;
        }
    }
}

const list = new LinkedList();

console.log("Size: ",list.size)
list.display();
list.insert(10,0);
list.insert(5,0);
list.insert(25,1);
list.insert(100,1);
list.insertBefore(25,999);
list.removeData(10)
list.display();
console.log("Size: ",list.size)


```
