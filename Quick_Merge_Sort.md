# Quicksort Algorithm

The quicksort algorithm works by following these steps:

1. **Choose a Pivot**: Select an element from the array to serve as the "pivot". Typically, the last element is chosen as the pivot.

2. **Partition**: Go through the rest of the array and compare each element to the pivot. If the element is smaller than the pivot, add it to the `left` array; if it's larger, add it to the `right` array.

3. **Recursion**: Recursively apply the quicksort algorithm to the `left` and `right` arrays. This involves repeating steps  1 and  2 for each of the subarrays until they are empty (i.e., contain only one element).

4. **Combine**: Once all subarrays are sorted, combine them by concatenating the `left`, pivot, and `right` arrays to create the final sorted array.

Here's a simplified explanation of the given quicksort function in English:

- If the array is empty or contains only one element (`arr.length <=  1`), it's already sorted, so just return the array.
- Pick the last element of the array as the pivot.
- Create two new empty arrays, `left` and `right`.
- Iterate over the array, comparing each element to the pivot. Add elements smaller than the pivot to the `left` array and elements larger than the pivot to the `right` array.
- After partitioning the array, recursively sort the `left` and `right` arrays by calling `quickSort()` on them.
- Concatenate the sorted `left` array, the pivot, and the sorted `right` array to form the fully sorted array.

```javascript

function quickSort(arr){
    if(arr.length<=1){
        return arr;
    }
    let pivot = arr[arr.length-1];
    let left=[];
    let right=[];
    for(let i = 0 ;i<arr.length-1 ; i++){
        if(arr[i]<pivot){
            left.push(arr[i]);
        }else{
            right.push(arr[i]);
        }
    }
   return [...quickSort(left),pivot,...quickSort(right)]
}


console.log("1:",quickSort([11,12,8,70,4,18]))
console.log("2:",quickSort([]))
console.log("3:",quickSort([11,4]))

```
# Merge Sort

Steps:-

1. **Find Mid Floor.**
2. **Make 0 to mid as leftArr and remaining as rightArr.**
3. **Recursively Continue the process till array size get 1**

**Merge it:-**
1. **Create an empty array "sortedArr"**

    *Till the size of left & right array gets null contuie the process*
2. **if first ele in leftArr is small add(push) to the sortedArr and remove that first ele from that leftArr else it will recheck and no sorting will happens!**
3. **if first ele in rightArr is small add(push) to the sortedArr and remove that first ele from that rightArr else it will recheck and no sorting will happens!**
4. **Return the reasult by spreading it, if any values available in the leftArr and RightArr merge it as Well!**


```javaScript
function mergeSort(arr){
    if(arr.length<2)return arr;
    let mid=Math.floor(arr.length / 2);
    
    let leftArr=arr.slice(0,mid);
    let rightArr = arr.slice(mid);
    return merge(mergeSort(leftArr),mergeSort(rightArr))
}
function merge(leftArr,rightArr){
    let sortedArr=[];
    while(leftArr.length && rightArr.length){
        if(leftArr[0]<=rightArr[0]){
            sortedArr.push(leftArr.shift());
        }else{
            sortedArr.push(rightArr.shift())
        }
    }
    return [...sortedArr,...leftArr,...rightArr]
}

console.log(mergeSort([8,20,-2,-4,-6]))
 
```

