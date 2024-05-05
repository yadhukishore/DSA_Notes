## 1. Given an array of size N. The task is to find the maximum and the minimum element of the array using the minimum number of comparisons.

### Basic Approach:-
```javascript
 function setMini(array){
    let min = Infinity;
    for(let i=0;i<array.length;i++){
        if(array[i]<min){
            min =array[i];
        }
    }
    return min;
}

function setMax(array){
    let max= -Infinity;
    for(let i=0;i<array.length;i++){
        if(array[i]>max){
            max=array[i];
        }
    }
    return max;
}

console.log(setMax([4,9,6,5,2,3]))

```
Time Complexity: O(N)

Auxiliary Space: O(1)


# Best implementation:-

```javascript

function getMinMax(arr){
    const minmax={};
    arr.sort((a,b)=>a-b);
    
    minmax.min = arr[0];
    minmax.max = arr[arr.length-1];
    return minmax;
}
console.log(getMinMax([1000,11,445,500,330,3000]))

```
Time complexity: O(n log n), where n is the number of elements in the array, as we are using a sorting algorithm.


Auxilary Space: is O(1), as we are not using any extra space.
