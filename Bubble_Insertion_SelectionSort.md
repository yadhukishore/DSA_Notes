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
