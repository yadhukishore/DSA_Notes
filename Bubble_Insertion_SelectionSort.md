# BubbleSort

Algo:
1. **for loop checks the max ele in the entire array and put in the end of the array**
2. **after exiting the for loop swapped value is true so it check the for loop again from the begining and find the next max ele and put in the second end of the array**
3. **Continue the process**

```javascript
function bubbleSort(arr){
    if(arr.length===0){
        return null;
    }
    else if(arr.length===1){
        return arr;
    }
    else{
        let swapped;
        do{
            swapped=false;
   for(let i=0;i<arr.length-1;i++){
       if(arr[i]>arr[i+1]){
           [arr[i],arr[i+1]]=[arr[i+1],arr[i]];
           swapped=true;
       }
   }
        }while(swapped)
        return arr;
    }
    
}

console.log("1: ",bubbleSort([2,3,66,11,55,37,9]))
console.log("2: ",bubbleSort([]))
console.log("3: ",bubbleSort([100]))
```
## timeComplexity of Bubble Sort
The time complexity of Bubble Sort varies depending on the scenario:

- **Best Case**: O(N)
  - This occurs when the array is already sorted. There are no swaps needed, and the algorithm only needs to make N-1 comparisons to confirm the array is sorted [0][1][2].

- **Average Case**: O(N^2)
  - The number of comparisons is constant in Bubble Sort. Regardless of the arrangement of elements, the number of comparisons is the same for each element, leading to O(N^2) comparisons [0][1][2].

- **Worst Case**: O(N^2)
  - This happens when the array is sorted in reverse order. The algorithm will have to make the maximum number of comparisons and swaps, which is N(N-1)/2 for both, resulting in O(N^2) time complexity [0][1][2].

The reason for the O(N^2) complexity in the worst and average cases is that Bubble Sort compares each pair of adjacent elements and swaps them if they are in the wrong order. This process is repeated for each element, leading to a quadratic number of operations in the worst-case scenario where the array is sorted in reverse order. In the average case, the number of operations is also quadratic due to the constant number of comparisons made for each element.

The space complexity of Bubble Sort is O(1), which means it uses a constant amount of additional space. This is because Bubble Sort is an in-place sorting algorithm, and it only uses a single additional memory space for temporary storage during swapping [0][1][2].

# Insertion Sort

Algo:-

1. **We need to assume as 2 arrays, right as unsorted and left as sorted**
2. **So the first ele is considered as sorted , So start loop from Second ele, and that ele is we need to put in the sorted array**
3. **Compare the ele we need to insert with the sorted array, is the sorted array's ele is greater till decrementing to 0:- Shift ele to the right**
4. **When the condition fails add it to the right side of the failed position**



```javascript
function insertionSort(arr){
    for(let i=1;i<arr.length;i++){
        let needToInsert=arr[i];
     let j=i-1;   
     while(j>=0&&arr[j]>needToInsert){
         arr[j+1]=arr[j];
         j--;
     }
     arr[j+1]=needToInsert;
    }
    return arr;
}

console.log("1:",insertionSort([11,12,8,70,4,18]))
console.log("2:",insertionSort([]))
console.log("3:",insertionSort([11,4]))
```

## Can you think of any optimizations to improve the performance of insertion sort? Implement them and analyze their impact.

### Optimizations for Insertion Sort

There are a few optimizations that can be applied to improve the performance of insertion sort:

1. **Binary Search for Insertion**: Instead of linearly searching for the correct position to insert an element, we can use binary search to find the insertion point more efficiently. This can reduce the number of comparisons needed to find the correct position, especially for larger arrays.

2. **Insertion Sort with Binary Search**: Combining binary search with insertion sort, we can perform a binary search to find the correct position to insert each element, and then shift elements to make space for the new element. This can further reduce the number of comparisons and overall runtime of the algorithm.

3. **Threshold for Linear Search**: For smaller subarrays, it might be more efficient to use linear search instead of binary search. We can set a threshold below which linear search is used, and above which binary search is used. This avoids the overhead of binary search for very small arrays.

Let's implement these optimizations and analyze their impact:

```javascript
// Insertion sort with binary search optimization
function insertionSort(arr) {
    for (let i = 1; i < arr.length; i++) {
        let key = arr[i];
        let left = 0;
        let right = i - 1;

        // Binary search to find the correct position to insert key
        while (left <= right) {
            let mid = Math.floor((left + right) / 2);
            if (arr[mid] > key) {
                right = mid - 1;
            } else {
                left = mid + 1;
            }
        }

        // Shift elements to make space for key
        for (let j = i - 1; j >= left; j--) {
            arr[j + 1] = arr[j];
        }

        // Insert key into correct position
        arr[left] = key;
    }
    return arr;
}

// Test the optimized insertion sort with binary search
let arr = [5, 2, 4, 6, 1, 3];
console.log("Original array:", arr);
console.log("Sorted array:", insertionSort(arr));
```
## Insertion sort Time complexity:-

The time complexity of Insertion Sort is as follows:

- **Best Case**: O(N)
  - This occurs when the array is already sorted. In this case, the algorithm only needs to make one comparison per element, leading to a linear number of operations [0][4].

- **Average Case**: O(N^2)
  - The average case is also quadratic. This is because, on average, each insertion must traverse half the currently sorted list while making one comparison per step. The list grows by one each time, and the number of traversals increases quadratically [3][4].

- **Worst Case**: O(N^2)
  - The worst-case scenario is when the array is sorted in reverse order. In this case, every iteration of the inner loop will scan and shift the entire sorted subsection of the array before inserting the next element, leading to a quadratic number of operations [0][3][4].

The reason for the O(N^2) complexity in the worst and average cases is that Insertion Sort compares each element with all the elements before it to find the correct position for insertion. In the worst case, where the array is sorted in reverse order, each element must be compared with all the previously sorted elements, resulting in a quadratic number of comparisons and shifts. In the average case, the number of comparisons is also quadratic due to the nature of the algorithm's operation [3][4].

The space complexity of Insertion Sort is O(1), which means it uses a constant amount of additional space. This is because Insertion Sort is an in-place sorting algorithm, and it only uses a single additional memory space for temporary storage during shifting of elements [0][2].

# Selection Sort
### Algorithm:-

1. **itreate through the unsorted array and find its minimum element with 2 pointers and change the minIndex with most min value in the array.**
2. **if the minIndex is changed swap the minindex with current i value in each iteration.**

```javascript

function selectionSort(arr) {
    if (arr.length <= 1) {
        return arr;
    } else {
        for(let i=0;i<arr.length-1;i++){
                let minIndex =i;
                for(let j=i+1;j<arr.length;j++){
                    if(arr[j]<arr[minIndex]){
                        minIndex=j
                    }
                }
                if(minIndex !==i){
                    [arr[i],arr[minIndex]]=[arr[minIndex],arr[i]];
                }
            }
            return arr;
        
    }
}

// Example usage:
console.log("1:",selectionSort([11,12,8,70,4,18]))
console.log("2:",selectionSort([]))
console.log("3:",selectionSort([11,4]))
```

## time complexity of selection Sort!

The time complexity of Selection Sort is as follows:

- **Best Case**: O(N^2)
  - The best-case scenario for Selection Sort is when the array is already sorted. However, even in this case, the algorithm still performs a full scan of the array to verify that it is sorted, which results in O(N^2) time complexity [0][1][2][3].

- **Average Case**: O(N^2)
  - The average case for Selection Sort is when the array elements are in a random order. This is because, regardless of the initial arrangement, the algorithm will always perform the same number of comparisons and swaps, resulting in a quadratic time complexity [0][2][3].

- **Worst Case**: O(N^2)
  - The worst-case scenario occurs when the array is sorted in reverse order. Even in this case, the algorithm must perform all the comparisons and swaps, leading to a quadratic time complexity [0][2][3].

The reason for the O(N^2) complexity in all cases is due to the nature of the Selection Sort algorithm. It consists of two nested loops: the outer loop iterates over each element in the array, and the inner loop finds the minimum element from the unsorted subarray. The inner loop performs N comparisons for the first element, N-1 for the second, and so on, until  1 for the last element. This results in a total of N(N-1)/2 comparisons, which simplifies to O(N^2) [0][2][3].

The space complexity of Selection Sort is O(1), which means it uses a constant amount of additional space. This is because Selection Sort is an in-place sorting algorithm and does not require any extra space other than a temporary variable for swapping [0][2][3].
