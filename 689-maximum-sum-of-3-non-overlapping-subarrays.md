Here is my video explainig it: https://youtu.be/Npjz9so97r8
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */

// Time: O(n)
// Space: O(n)
var maxSumOfThreeSubarrays = function(nums, k) {
    // k = 1
    // [1,2,1,2,6,7,5,1]  3 numbers sums up to the largest
  
    // [1,2,1,2,6,7,5,1]  1 number => O(n)
    // [1,2,1,2,6,7,5,1]  2 numbers
   
    // n(n - 1) * 2 => n^2
    // cache the max out of subarray from right left
    // loop from left to right, and get the result
    // could be improved to O(2n) => O(n)
  
    // [1,2,1,2,6,7,5,1]  3 numbers
  
    // O(n^2)
    // O(n) + O(n) + O(n) => O(n)
  
    // 1. crush it into k = 1 array
    // slide window
    const sums = []
    let sum = 0
    for (let i = 0; i < nums.length; i++) {
      sum += nums[i]
      if (i >= k) {
        sum -= nums[i - k]
      }
      
      if (i >= k - 1) {
        sums.push(sum)
      }
    }
    
    // 2. max Array from left(inclusive)
    const maxIndexFromLeft = Array(sums.length).fill(0)
    maxIndexFromLeft[0] = 0
    for (let i = 1; i < sums.length; i++) {
      if (sums[i] > sums[maxIndexFromLeft[i - 1]]) {
        maxIndexFromLeft[i] = i
      } else {
        maxIndexFromLeft[i] = maxIndexFromLeft[i - 1]
      }
    }
    
    // 3. max array from right
    const maxIndexFromRight = Array(sums.length).fill(0)
    maxIndexFromRight[sums.length - 1] = sums.length - 1
    for (let i = sums.length - 2; i > -1; i--) {
      if (sums[i] >= sums[maxIndexFromRight[i + 1]]) {
        maxIndexFromRight[i] = i
      } else {
        maxIndexFromRight[i] = maxIndexFromRight[i + 1]
      }
    }
  
    // 4. get the right by fixing middle element
    let max = -Infinity
    let result = null
    for (let i = k; i < sums.length - k; i++) {
      const sum = sums[maxIndexFromLeft[i - k]] + sums[i] + sums[maxIndexFromRight[i + k]]
      if (sum > max) {
        max = sum
        result = [maxIndexFromLeft[i - k], i, maxIndexFromRight[i + k]]
      }
    }
    return result
};
```
