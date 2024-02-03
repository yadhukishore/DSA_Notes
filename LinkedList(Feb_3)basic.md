## linked list with tail:-

```javascript
class Node{
    constructor(data){
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
        const newNode= new Node(data);
        if(!this.head){
            this.head=newNode;
            this.tail=newNode;
        }else{
            newNode.next=this.head;
            this.head=newNode;
        }this.size++;
    }
    append(data){
        const newNode = new Node(data);
         if(!this.head){
            this.head=newNode;
            this.tail=newNode;
        }else{
           this.tail.next = newNode;
            this.tail = newNode;
        }
        this.size++;
    }
    
    
    removeFrom(pos){
        if(pos<0 || pos >= this.size){
            return null;
        }
        let removedNode;
        if(pos === 0){
            removedNode=this.head;
            this.head = this.head.next;
             if (!this.head) {
            this.tail = null;
        }
        }else{
            let prev = this.head;
            for(let i =0 ; i < pos-1 ; i++){
                prev = prev.next;
            }
            removedNode = prev.next;
            prev.next = removedNode.next;
             if (!removedNode.next) {
            this.tail = prev;
        }
        }
        this.size--;
        return removedNode.value;
    }
    
    insert(data,pos){
        if(pos<0 || pos >this.size){
            return console.log("Pos invalid!")
        }
     if(pos === 0){
            this.add(data);
        }
        else{
            const newNode = new Node(data);
            let prev = this.head;
            for(let i=0 ; i<pos-1 ; i++){
                prev = prev.next;
            }
            newNode.next = prev.next;
            prev.next = newNode;
            this.size++;
        }
        
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
            console.log("List IS Empty!");
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
console.log("size: ",list.size);
list.display();


list.add(300);
list.add(200);
list.add(100);
list.append(10)
// list.removeFrom(3)
list.insert(4,4)
// list.removeData(100);
list.reverse();
list.display();
console.log("size: ",list.size);


```
