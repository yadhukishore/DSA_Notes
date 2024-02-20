To create a Markdown file for these JavaScript functions and their output, you can follow this format:

```markdown
# JavaScript Functions

## itemsCommon(arr1, arr2)

```javascript
function itemsCommon(arr1, arr2) {
    let obj = {};
    for (let i = 0; i < arr1.length; i++) {
        obj[arr1[i]] = true;
    }
    for (let j = 0; j < arr2.length; j++) {
        if (obj[arr2[j]]) {
            return true;
        }
    }
    return false;
}

console.log("itemsCommon:", itemsCommon([1, 3, 5], [2, 4, 5]));
```

## twoSum(arr, t)

```javascript
function twoSum(arr, t) {
    let hashT = {};
    for (let i = 0; i < arr.length; i++) {
        const complement = t - arr[i];
        if (hashT[complement] !== undefined) {
            return [hashT[complement], arr[i]];
        }
        hashT[arr[i]] = arr[i];
    }
    return [];
}

console.log("twoSum:", twoSum([1, 2, 3, 4], 5));
```

## groupAnagrams(strs)

```javascript
var groupAnagrams = function(strs) {
    const anagrams = new Map();
    for (const val of strs) {
        const sortedStr = val.split('').sort().join('');
        if (anagrams.has(sortedStr)) {
            anagrams.get(sortedStr).push(val);
        } else {
            anagrams.set(sortedStr, [val]);
        }
    }
    return Array.from(anagrams.values());
};

const strs = ["eat", "tea", "tan", "ate", "nat", "bat"];
console.log("groupAnagrams:", groupAnagrams(strs));
```

## isAnagram(a, b)

```javascript
function isAnagram(a, b) {
    if (a.length !== b.length) return false;
    const freqCountA = {};
    const freqCountB = {};
    for (let valA of a) {
        freqCountA[valA] = (freqCountA[valA] || 0) + 1;
    }
    for (let valB of b) {
        freqCountB[valB] = (freqCountB[valB] || 0) + 1;
    }
    for (let value in freqCountA) {
        if (freqCountA[value] !== freqCountB[value]) return false;
    }
    return true;
}

console.log(isAnagram("anagram", "nagaram"));
```



## Word Frequency Counter

```markdown
# JavaScript Functions

## Word Frequency Counter

```javascript
// Word Frequency Counter: Write a function that takes in a string and returns a hash table where the keys are unique words in the string and the values are the frequencies of those words.
function wordFrequencyCounter(str) {
    const words = str.split(' ');
    const frequencyCount = {};
    for (let word of words) {
        frequencyCount[word] = (frequencyCount[word] || 0) + 1;
    }
    return frequencyCount;
}

const str = "Hai I am a good boy and a good progreammer";
console.log("wordFrequencyCounter", wordFrequencyCounter(str));
```

## Isomorphic Strings

```javascript
// Isomorphic Strings: Given two strings s and t, determine if they are isomorphic. Two strings are isomorphic if the characters in s can be replaced to get t. All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character, but a character may map to itself.
function isIsomorphic(s, t) {
    if (s.length !== t.length) return false;
    const mapS = {};
    const mapT = {};
    for (let i = 0; i < s.length; i++) {
        const valS = s[i];
        const valT = t[i];
        if (mapS[valS] === undefined && mapT[valT] === undefined) {
            mapS[valS] = valT;
            mapT[valT] = valS;
        } else if (mapS[valS] !== valT || mapT[valT] !== valS) {
            return false;
        }
    }
    return true;
}

// Example usage:
console.log(isIsomorphic("badc", "kikp")); // Output: false
console.log(isIsomorphic("foo", "baa")); // Output: true
console.log(isIsomorphic("foo", "bia"));
```

## First Unique Character in a String

```javascript
function firstUniqChar(str) {
    const charFreq = {};
    for (let val of str) {
        charFreq[val] = (charFreq[val] || 0) + 1;
    }
    for (let i = 0; i < str.length; i++) {
        if (charFreq[str[i]] === 1) {
            return i;
        }
    }
    return -1;
}

console.log("firstUniqChar", firstUniqChar("leetcode"));
```
## secondUnique char:-

```javascript

function secondUniqChar(strg) {
    const charFreq = {};
    let uniqueCount = 0; // Counter for unique characters
    
    // Count the frequency of each character in the string
    for (let val of strg) {
        charFreq[val] = (charFreq[val] || 0) + 1;
    }
    
    // Iterate through the string to find the second unique character
    for (let i = 0; i < strg.length; i++) {
        if (charFreq[strg[i]] === 1) {
            uniqueCount++; // Increment the count of unique characters
            if (uniqueCount === 2) {
                return i; // Return the index of the second unique character
            }
        }
    }
    
    return -1; // If no second unique character is found, return -1
}

console.log(secondUniqChar("leetcode")); // Output: 3 (index of the second unique character 't')
```

