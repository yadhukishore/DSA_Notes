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
The time complexity of quicksort varies depending on the case:

- **Best Case**: The best case occurs when the pivot element is always the median of the array, leading to a balanced partition at each step. This results in a time complexity of O(N log N). The reason for this efficiency is that the partitioning step divides the array into two nearly equal halves, which then leads to a logarithmic number of levels in the recursion tree. Each level of the tree represents a partition operation, and the cost of each level is linear in the size of the partition, leading to a total time complexity of O(N log N) [0][2].

- **Average Case**: In the average case, the array elements are in a "jumbled" order that is neither ascending nor descending. Despite the lack of a specific pattern, quicksort still performs well, maintaining a time complexity of O(N log N). This is because, on average, each partition step will split the array into two parts of roughly equal size, leading to a balanced recursion tree. The depth of this tree is logarithmic, and the work done at each level (partitioning) is linear, thus the overall time complexity remains O(N log N) [2].

- **Worst Case**: The worst case happens when the pivot element is either the smallest or the largest element in the array, leading to highly unbalanced partitions. In such a scenario, one partition contains N-1 elements, and the other contains  0, resulting in a time complexity of O(N^2). This occurs because the depth of the recursion tree becomes linear, and at each level, the partitioning step takes linear time. The total time complexity is the sum of the time taken at each level of the recursion tree, which sums up to N^2 [0][3].

The space complexity of quicksort is O(log N) due to the space required for the call stack during the recursive partitioning. Each recursive call adds a level to the call stack, and in the worst case, this can go as deep as log N levels. However, it's important to note that this space is used for storing the recursive calls themselves, not the data being sorted [0].

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

## time Complexity of merge sort

The time complexity of merge sort is O(N log N) in all cases: best, average, and worst. This uniformity across all cases is due to the algorithm's divide-and-conquer approach, which involves dividing the array into two halves until it reaches subarrays of size  1, then merging these subarrays back together in a sorted order.

- **Divide Phase**: The array is recursively divided into two halves until each subarray contains only one element. This division process takes log(N) time as it involves splitting the array log(N) times until it reaches the base case.
- **Conquer Phase**: Once the array is divided, the merge process begins. Each merge operation takes linear time, O(N), because it involves comparing and merging elements from the two halves.
- **Combine Phase**: The merge operations are performed in a way that ensures the entire array is sorted, which also takes log(N) time due to the depth of the recursive calls.

Therefore, the overall time complexity is dominated by the merge operations, which take O(N) time each, and there are log(N) levels of recursion. Hence, the total time complexity is O(N log N) [0][1].

The space complexity of merge sort is O(N), as it requires additional space to hold the temporary arrays used during the merge process [0][1]. This is because, unlike some other sorting algorithms like quicksort, merge sort does not sort the array in place. Instead, it uses extra space to create temporary arrays for merging.
