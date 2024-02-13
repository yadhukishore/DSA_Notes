# Hash Table
**A hash table, also known as hash map, is a data Structure i.e used to store key value pairs.**

**Given a key, we can assosiate a value with that key for faster Lookup**

***JavaScript Objects also have same Purpose?    Yes its a special implementaion of hash table DS***

In JavaScript, objects can indeed be used as hash tables. In fact, when you create an object and add key-value pairs to it, you are essentially using it as a hash table. However, when people refer to hash tables in JavaScript, they are often talking about using plain JavaScript objects (`{}`) specifically for the purpose of storing key-value pairs in a way that emphasizes the hashing mechanism for efficient access.

Here are a few reasons why people may explicitly use the term "hash table" in JavaScript:

1. **Emphasis on Key-Value Pairs:** Using the term "hash table" highlights the primary purpose of the object, which is to store key-value pairs, rather than just being a generic object.

2. **Performance Considerations:** Hash tables, implemented using objects in JavaScript, offer fast lookups. Retrieving, inserting, and deleting elements from a hash table (object) has an average time complexity of O(1), making it efficient for many use cases.

3. **Terminology Consistency:** Hash table is a well-known term in computer science and data structures, so using it provides clarity and consistency, especially when discussing algorithms and data structures across different programming languages.

4. **Hashing Mechanism:** Emphasizing the use of a hash table underscores the underlying mechanism of hashing, which is crucial for understanding how key-value pairs are stored and accessed efficiently.

So, while objects in JavaScript can function as hash tables, using the term "hash table" can provide clarity and emphasize the specific use of the object for storing key-value pairs with efficient lookup using hashing.

***Maps allows us to store key value pairs***

eg:-

1. **'in'=> india     ,in is the key India is the value**
2. **'au'=> asustralia , au is the key austerlia is the value**

these need to be stored for fast look up. **if i specify a key as 'in' i should retrive India.**

1. **We store the key value pairs in a fixed sized array!**
2. **Arrays have numeric index**
3. **Remove to delete a key value pair**

**How do we go from using a string as an index tooo number as an index?**

### A hashing function accepts the string key, converts it into a hash code using a defined logic! and then maps it into a numeric index that is within the bounds of the array Using the index, store the value. The Same Hashing function is reused to retrieve the value given a key!

1. **Set to store a key-value pair**
2. **Get to retrieve a value given its key**
3. **Remove to delete a key value pair**

### Hash Table Usage
1. **Hash tables are typically implemented where constant time lookup and insertion are required!**
2. **Flexible Key Types: Hash tables can support a wide range of key types, including strings, numbers, objects, and even complex data structures. This flexibility allows for versatile data storage and retrieval patterns.**
3. **Memory Efficiency: Hash tables consume memory proportional to the number of stored key-value pairs, making them memory-efficient for storing large datasets. Additionally, hash tables can dynamically resize to accommodate more elements while maintaining a relatively low memory overhead.**


## Algorithm

1. **Initialization**:
   - Initialize a hash table with a specified size.
   - Create an array called `table` to store key-value pairs.

2. **Hash Function** (`hash(key)`):
   - Accepts a key (string) as input.
   - Calculates a hash value for the key using a simple hash function.
   - The hash value is calculated by summing up the Unicode values of each character in the key and then taking the remainder when divided by the size of the hash table.

3. **Set Method** (`set(key, value)`):
   - Accepts a key and a value as input.
   - Calculates the index in the hash table where the key-value pair should be stored using the hash function.
   - Inserts the key-value pair at the calculated index in the hash table.

4. **Get Method** (`get(key)`):
   - Accepts a key as input.
   - Calculates the index in the hash table where the key-value pair is expected to be stored using the hash function.
   - Retrieves the value associated with the key at the calculated index in the hash table.
   - Returns the value, or `undefined` if the key is not found.

5. **Remove Method** (`remove(key)`):
   - Accepts a key as input.
   - Calculates the index in the hash table where the key-value pair is stored using the hash function.
   - Removes the key-value pair from the calculated index in the hash table by setting the value to `undefined`.

6. **Display Method** (`display()`):
   - Iterates over each slot in the hash table.
   - Prints out the index and the corresponding key-value pair if it exists (i.e., the value is not `undefined`).

This algorithm outlines the basic functionality of the provided hash table implementation, including setting key-value pairs, retrieving values by keys, removing key-value pairs, and displaying the contents of the hash table.

```javascript
class HashTable{
    constructor(size){
        this.table = new Array(size);
        this.size = size;
    }
    hash(key){
        let total=0;
        for(let i=0; i<key.length;i++){
            total +=key.charCodeAt(i);
        }
        return total%this.size;
    }
    set(key,value){
        const index =this.hash(key);
        this.table[index]=value;
    }
    get(key){
    const index = this.hash(key);
    if(!this.table[index]){
        console.log("Cant get!");
    }else{
        return this.table[index];
    }
    }
    remove(key){
        const index = this.hash(key);
        if(!this.table[index]){
            return false;
        }else{
            this.table[index]=undefined;
        }
    }
    
    display(){
        for(let i=0 ; i<this.table.length ; i++){
            if(this.table[i]!== undefined){
                console.log(i,this.table[i]);
            }
        }
    }
    
}
const table = new HashTable(50);
table.set("Name","Yadhu");
table.set("age",22);
table.display()
console.log(table.get("Name"))
console.log("After deletion:");
table.remove("age");
table.display();
```
## Leet Code on Hash Table:-

### 3005. Count Elements With Maximum Frequency

You are given an array nums consisting of positive integers.

Return the total frequencies of elements in nums such that those elements all have the maximum frequency.

The frequency of an element is the number of occurrences of that element in the array.

 

Example 1:

Input: nums = [1,2,2,3,1,4]

Output: 4

Explanation: The elements 1 and 2 have a frequency of 2 which is the maximum frequency in the array.
So the number of elements in the array with maximum frequency is 4.
Example 2:

Input: nums = [1,2,3,4,5]

Output: 5

Explanation: All elements of the array have a frequency of 1 which is the maximum.
So the number of elements in the array with maximum frequency is 5.

#### Algorithm

countElementsWithMaxFrequency(nums)

1. **Initialize a hash table called `frequencyMap` to store the frequency of elements.**
2. **Initialize `maxFrequency` to 0.**
3. **Iterate through each element `num` in the input array `nums`:**
    - If `frequencyMap[num]` exists, increment its value by 1. Otherwise, set `frequencyMap[num]` to 1.
    - Update `maxFrequency` to be the maximum of `maxFrequency` and the frequency of `num`.
4. **Initialize `count` to 0.**
5. **Iterate through each key `num` in `frequencyMap`:**
    - If the frequency of `num` equals `maxFrequency`, increment `count` by 1.
6. **Return the product of `count` and `maxFrequency`.**

```javascript
var maxFrequencyElements = function(nums) {
const frequencyMap = {};
let maxFrequency = 0;

for(let val of nums){
    frequencyMap[val] = (frequencyMap[val]||0)+1;
    maxFrequency=Math.max(maxFrequency,frequencyMap[val]);
}
let count = 0;
for(let val in frequencyMap){
    if(frequencyMap[val]===maxFrequency){
        count++;
    }
}
return count*maxFrequency;
}
```
