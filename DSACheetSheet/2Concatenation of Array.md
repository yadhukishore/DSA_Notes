# 1929. Concatenation of Array

Given an integer array `nums` of length n, you want to create an array ans of length 2n where `ans[i] == nums[i]` and `ans[i + n] == nums[i]` for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

**Example 1:**

Input: nums = [1,2,1]

Output: [1,2,1,1,2,1]

### Approach-1
```javascript
var getConcatenation = function(nums) {
	//spread the nums array twice and return it
    return [...nums,...nums]
};
```
### Approach-2
```javascript
var getConcatenation = function(nums) {
    const result = [];
    for(let i=0; i<nums.length;i++){
        result[i] = nums[i];
        result[i+nums.length]=nums[i];
    }
    return result;
};
```
