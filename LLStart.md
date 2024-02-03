## without tail

```javascript
class Node{
    constructor(data){
        this.data = data;
        this.next = null;
    }
}
class LinkedList{
    constructor(){
        this.head=null;
        this.size=0;
    }
    add(data){
        const newNode = new Node(data)
        if(!this.head){
            this.head = newNode;
        }else{
            newNode.next = this.head;
            this.head = newNode;
        }
        this.size++;
    }
    
    append(data){
        const newNode = new Node(data);
        if(!this.head){
            this.head = newNode;
        }else{
            let curr =this.head;
            while(curr.next){
                curr=curr.next;
            }
            curr.next = newNode;
        }
        this.size++;
    }
    
    insert(data,pos){
        if(pos<0 || pos > this.size){
            return console.log("Invalid Position!");
        }
        if(pos === 0){
            this.add(data);
        }else{
            const newNode = new Node(data);
            let prev = this.head;
            for(let i=0; i<pos-1;i++){
                prev = prev.next;
            }
            newNode.next=prev.next;
            prev.next=newNode;
            this.size++;
        }
    }
    
    removeFrom(pos){
        if(pos<0 || pos >= this.size){
            return null;
        }
        let removedNode;
        if(pos === 0){
            removedNode=this.head;
            this.head = this.head.next;
        }else{
            let prev = this.head;
            for(let i =0 ; i < pos-1 ; i++){
                prev = prev.next;
            }
            removedNode = prev.next;
            prev.next = removedNode.next
        }
        this.size--;
        return removedNode.value;
    }
    
    removeData(data){
        if(!this.head){
            return null;
        }
        if(this.head.data === data){
            this.head = this.head.next;
            this.size--;
            return data;
        }
        else{
            let prev = this.head;
            while(prev.next && prev.next.data !== data){
                prev = prev.next;
            }
            if(prev.next){
                let removedNode =prev.next;
                prev.next = removedNode.next;
                this.size--;
                return data;
            }
            return null;
        }
    }
    
    search(data){
        if(!this.head){
            return null
        }
        let i=0;
        let curr = this.head;
        while(curr){
            if(curr.data === data){
                return i;
            }
            curr = curr.next;
            i++;
        }
        return  -1
    }
   reverse(){
       let prev = null;
       let curr = this.head;
       while(curr){
           let next = curr.next;
           curr.next=prev;
           prev=curr;
           curr=next;
       }
       this.head = prev;
   }
    display(){
        if(!this.head){
            console.log("List is empty!");
        }else{
            let curr = this.head;
            while(curr){
                console.log(curr.data);
                curr=curr.next;
            }
        }
    }
}

const list = new LinkedList();
console.log('Size: ',list.size);
list.display();
list.insert(10,0);
list.display();
list.insert(20,0);
list.display();
list.insert(30,1);
list.display();
list.insert(40,2);
list.display();

console.log('New_Size: ',list.size);
list.display();
// console.log(list.search(20))
list.reverse();
list.display();

```
