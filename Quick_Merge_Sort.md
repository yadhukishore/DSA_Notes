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
The `quickSort` function you provided is indeed using recursion, but it's not an example of backtracking. Instead, it's an example of a divide-and-conquer algorithm.

In quicksort, the array is partitioned around a pivot element, and then the algorithm is recursively applied to the subarrays formed by the partition. The base case of the recursion occurs when the size of the array becomes 1 or less, at which point the array is considered sorted and returned.

Here's a breakdown of how recursion is used in the `quickSort` function:

1. **Base Case**: The function checks if the length of the array `arr` is 1 or less. If so, it returns the array as it is (already sorted).
   
2. **Partitioning**: If the array has more than one element, it selects a pivot (in this implementation, the last element) and partitions the array into two subarrays - `left` containing elements smaller than the pivot and `right` containing elements greater than or equal to the pivot.

3. **Recursion**: It then recursively calls `quickSort` on the `left` and `right` subarrays. This step sorts the subarrays.

4. **Combining**: Finally, it combines the sorted `left` subarray, the pivot, and the sorted `right` subarray to produce the sorted output.

Recursion is used here to break down the sorting problem into smaller subproblems, solve each subproblem independently, and then combine the solutions to obtain the final sorted array. This divide-and-conquer approach is a common pattern in recursive algorithms, and it's not limited to backtracking scenarios.
### Complexity
Sure, let's break it down in simpler terms:

1. **Best-case scenario:** 
   - Imagine you have a stack of cards you want to sort. Quick sort works best when each time you divide your stack into two roughly equal parts. Think of it like splitting a deck of cards in half.
   - If you keep dividing the stack in half until each part contains only one card (or is nearly equal in size), and then you start merging them back together, it won't take too long. This is because each step of dividing and merging takes \(O(n)\) time, and you only need to do about \(\log n\) steps. 
   - So, in total, it takes about \(O(n \log n)\) time, which is pretty fast.

2. **Worst-case scenario:** 
   - However, if you're unlucky and every time you try to split your stack, you end up with a really lopsided split, like one half is just one card and the other half is almost all of the cards. It's like trying to split a deck where all the big cards are on one side and all the small cards are on the other.
   - If this keeps happening, and you keep splitting and merging in this unbalanced way, it's going to take a long time. Each step of splitting and merging still takes \(O(n)\) time, but now you have to do a lot more steps because you're not making much progress dividing your stack in half each time. This is because you may need to do about \(n\) steps for each level of splitting.
   - So, in total, it can take \(O(n^2)\) time, which is much slower than \(O(n \log n)\).

3. **Average-case scenario:** 
   - In reality, when you're shuffling your cards, you're probably not always going to end up with perfectly balanced splits or extremely unbalanced splits. You might get some balanced, some unbalanced.
   - On average, if you randomly shuffle your cards and do the splitting and merging, you'll end up with a mix of good splits and bad splits. So, it usually takes about \(O(n \log n)\) time, which is reasonably fast.

In summary, quick sort is usually fast (\(O(n \log n)\)), but it can be slow in some cases (\(O(n^2)\)) if the splits are consistently unbalanced. However, on average, it performs well because it often gets reasonably balanced splits.

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

