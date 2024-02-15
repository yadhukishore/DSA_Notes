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
## Hash Table Collisions
### insted of storing one value at the given index we store an array of key value pairs

Lets Check an alogorith to avoid collitions:-

**In Set Method**

- **make the `this.table[index]` to a variable `bucket`.**
- **If there is no value stored in that index `!bucket`, create a array with key value pair `[[key,vale]]` and push it.**
- **If a value is already exist, check that the array contain sub array with same key using `find` by checking item key`item[0]` with the passed in key `key`.     If Such an item is present(key is equal) we the Update its value.**
- if not we push the key - value pair.

**In get Method**

- **make the `this.table[index]` to a variable `bucket`.**
- **if the bucket exist,we check that the array exist with the same key  by checking item key`item[0]` with the passed in key `key`.        If Such an item is present(key is equal) we `return` the value of the item `sameItemKey[1]` (key is syored at index 0 and value is stored at index 1, so [1])**
- else bucket not exist we return `undefined` indicating the key does not exist!

**In remove Method**

- **if the bucket exist,we check that the array exist with the same key  by checking item key`item[0]` with the passed in key `key`.         If Such an item is present(key is equal) we use `array.splice()` to remove the item from the array!**
- **`bucket.splice(bucket.indexOf(sameKeyItem), 1);` The splice method takes two parameters: the index at which to start removing elements and the number of elements to remove. In this case, splice is called with the index of the found item (bucket.indexOf(sameKeyItem)) and 1 as the number of elements to remove (since we want to remove only one item).**


*Code:-*
```javascript
class HashTable{
    constructor(size){
        this.table = new Array(size);
        this.size = size;
    }
    hash(key){
        let total = 0;
        for(let i =0 ; i<key.length;i++){
            total+=key.charCodeAt(i);
        }
        return total % this.size
    }
    set(key,value){
        const index = this.hash(key);
        // this.table[index] = value;
        const bucket = this.table[index];
        if(!bucket){
            this.table[index] =[[key,value]];
        }else{
            const sameKeyItem = bucket.find(item=>item[0] === key)
            if(sameKeyItem){
                sameKeyItem[1] = value;//update
            }else {
                bucket.push([key,value]);
            }
        }
    }
    get(key){
        const index = this.hash(key);
        // return this.table[index];
        const bucket = this.table[index];
        if(bucket){
            const sameKeyItem = bucket.find(item=>item[0] === key)
            if(sameKeyItem){
                return sameKeyItem[1];//key is stored in index0 and value is stored at index 1.
            }else{
                return undefined;
            }
        }
    }
    
    remove(key){
        const index = this.hash(key);
        const bucket = this.table[index];
        if(bucket){
            const sameKeyItem = bucket.find(item=>item[0]  ===  key)
            if(sameKeyItem){
                bucket.splice(bucket.indexOf(sameKeyItem),1);
            }
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
table.set("name","Yadhu");
table.set("age",22);
table.display();

console.log(table.get("name"));
table.set("Sname","Thaju");
table.set("name","Kishore");
table.remove("name")
table.display();
```

### Time complexity of collitions in Hash Table
**In all the above Methods we used `array.find` which loops over the elements in the array-> its time complexity O(n), However in Hash tables the collitions are very minimal and it can be reduced to a Great extend by having better hashing functions, So that we generally consider the average case time complexity insted of worst case when it comes to hash table. So the average case time complexity is constant O(n), i.e the hash tables are choosen mostly when solving problems!**

# Leet Code on Hash Table:-

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

## 645. Set Mismatch

**You have a set of integers s, which originally contains all the numbers from 1 to n. Unfortunately, due to some error, one of the numbers in s got duplicated to another number in the set, which results in repetition of one number and loss of another number.**

**You are given an integer array nums representing the data status of this set after the error.**

**Find the number that occurs twice and the number that is missing and return them in the form of an array.**

 

Example 1:

Input: nums = [1,2,2,4]
Output: [2,3]
Example 2:

Input: nums = [1,1]
Output: [1,2]

To solve the Set Mismatch problem on LeetCode using hashtables in JavaScript, follow these steps:

1. Create an empty hashtable or object to keep track of the occurrences of each number in the array.
2. Iterate through the array, and for each element:
   - Check if the current number exists in the hashtable.
   - If it does, remove it from the hashtable.
   - If it doesn't, add it to the hashtable.
3. After iterating through the array, any remaining entry in the hashtable represents the duplicate number, and the missing number would be the one that is not present in the hashtable.

Here's a sample code snippet to illustrate the solution:

```javascript
function findErrorNums(nums) {
    const numCounts = {};
    let duplicate = null;

    for (let num of nums) {
        if (numCounts[num]) {
            duplicate = num;
        } else {
            numCounts[num] = true;
        }
    }

    let missing = null;
    for (let i =  1; i <= nums.length; i++) {
        if (!numCounts[i]) {
            missing = i;
            break;
        }
    }

    return [duplicate, missing];
}
```

In this code:

- `numCounts` is the hashtable where keys represent the numbers in the array, and the presence of a key indicates that the number has appeared in the array.
- `duplicate` is initially set to `null` and gets assigned the duplicate number once found.
- `missing` is initially set to `null` and gets assigned the missing number once found.
- The loop checks each number in the array against the hashtable. If a number is found more than once, it is marked as the duplicate. If a number is not found in the hashtable after the loop completes, it is marked as the missing number.
- The function finally returns an array containing the duplicate and missing numbers.



## 290. Word Pattern

Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

 

Example 1:

Input: pattern = "abba", s = "dog cat cat dog"
Output: true
Example 2:

Input: pattern = "abba", s = "dog cat cat fish"
Output: false
Example 3:

Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false





To solve the Word Pattern problem using hashtables in JavaScript, you can follow these steps:

1. Initialize two empty objects (which act as hashtables) to keep track of the mapping between words and patterns.
2. Iterate over the words and patterns simultaneously. For each word and corresponding pattern:
   - Check if the word is already mapped to a pattern in the first hashtable (`wordToPattern`).
   - If it is, ensure that the mapped pattern matches the current pattern. If they don't match, return `false`.
   - If the word isn't mapped yet, check if the pattern is already mapped to a word in the second hashtable (`patternToWord`).
   - If it is, ensure that the mapped word matches the current word. If they don't match, return `false`.
   - If neither condition is met, map the word to the pattern and vice versa.
3. If you finish iterating without returning `false`, return `true` since all words and patterns matched correctly.

Here's a JavaScript code snippet that demonstrates this approach:

```javascript
function wordPattern(pattern, str) {
    const wordList = str.split(' ');
    if (pattern.length !== wordList.length) {
        return false;
    }
    
    const wordToPattern = {};
    const patternToWord = {};
    
    for (let i =  0; i < pattern.length; i++) {
        const word = wordList[i];
        const p = pattern[i];
        
        if (wordToPattern[word]) {
            if (wordToPattern[word] !== p) {
                return false;
            }
        } else {
            if (patternToWord[p]) {
                if (patternToWord[p] !== word) {
                    return false;
                }
            } else {
                wordToPattern[word] = p;
                patternToWord[p] = word;
            }
        }
    }
    
    return true;
}
```

In this code:

- `wordToPattern` maps words to patterns.
- `patternToWord` maps patterns to words.
- We first split the `str` into words using `split(' ')`.
- We then iterate over the `pattern` and `wordList` simultaneously.
- At each iteration, we check if the current word or pattern is already mapped to something else. If they are, we compare the mappings to see if they match. If they don't, we return `false`.
- If there are no conflicts, we map the word to the pattern and vice versa.
- If we finish the loop without returning `false`, we return `true` indicating that the string follows the pattern.

## 1.Two Sum

Certainly! Here's a breakdown of the `twoSum` algorithm:

1. **Initialization**:
   - The algorithm takes in an array of numbers `nums` and a target integer `target`.

2. **HashMap Initialization**:
   - A hash map `hashMap` is initialized to store the indices of numbers encountered so far. It will map each number to its index in the array.

3. **Iterating through the Array**:
   - The algorithm iterates through the `nums` array using a loop, starting from the first element (index 0) and moving to the last element.
   
4. **Calculating Complement**:
   - For each number `nums[i]`, it calculates the complement, which is the difference between the `target` and the current number (`complement = target - nums[i]`).
   
5. **Checking if Complement Exists**:
   - It checks if the `complement` exists in the `hashMap` by looking it up with `hashMap[complement]`.
   
6. **Returning the Indices**:
   - If the complement exists in the hash map (i.e., `hashMap[complement]` is not `undefined`), it means that there is a pair of indices (stored in `hashMap[complement]` and `i`) whose corresponding numbers sum up to the target.
   - In this case, it returns an array containing the indices of the two numbers.
   
7. **Updating HashMap**:
   - If the complement does not exist in the hash map, it means that the current number does not have a complement encountered earlier in the array.
   - In such a case, it adds the current number and its index to the hash map (`hashMap[nums[i]] = i`).
   
8. **Returning Empty Array**:
   - If the loop completes without finding a pair of numbers that sum up to the target, the algorithm returns an empty array, indicating that no such pair was found.

In summary, the algorithm efficiently finds a pair of indices of numbers in the input array that sum up to the target using a hash map to store the indices of numbers encountered so far. It has a time complexity of O(n), where n is the number of elements in the input array.

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
    const hashMap = {};
    for(let i =0 ;i<nums.length ; i++){
        const complement = target-nums[i];
        if(hashMap[complement]!==undefined){
            return [hashMap[complement],i];
        }
        hashMap[nums[i]]=i;
    }
    return [];
};
