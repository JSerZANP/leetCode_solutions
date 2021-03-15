
Here is a video explaining: https://www.youtube.com/watch?v=-5-4t4S0LOg

```js
/**
 * @param {number[]} nums
 * @param {number} x
 * @return {number}
 */

// TLE with recursion
// 0 * n + 1 * (n - 1) + 2 * (n - 2) + ... n * 0
// O(n^2) ~ O(n^3) 
// const minOp = (arr, start, end, target) => {
//   if (target === 0) return 0
//   if (start > end || target < 0) return Infinity
//   const withLeft = minOp(arr, start + 1, end, target - arr[start])
//   const withRight = minOp(arr, start, end - 1, target - arr[end])
//   return Math.min(withLeft + 1, withRight + 1)
// }

// var minOperations = function(nums, x) {
//   const result = minOp(nums, 0, nums.length - 1, x)   
//   return result === Infinity ? -1 : result
// };

// [i1] [i2] [i3 ] 
// Sum(i1) + Sum(i3) = target, ane len(i1) + len(i3) smallest
// Sum(i) = Sum(i - 1) + nums[i]


// 1. cache sum from right, map<sum, index>
// 2. get sum from left, check index from above map for target - sum
//    - update the longest distance
var minOperations = function(nums, x) {
  let result = Infinity
      
      
  const sumRight = new Map([[0, nums.length]])
  let temp = 0
  for (let i = nums.length - 1; i >= 0; i--) {
    temp += nums[i]
    sumRight.set(temp, i)
  }
  
  temp = 0
  for (let i = -1; i < nums.length; i++) {
    temp += i < 0 ? 0 : nums[i]
    
    if (temp > x) break
    
    const possibleIndex = sumRight.get(x - temp)
    if (possibleIndex !== undefined && possibleIndex > i) {
      const steps = i + 1 + (nums.length - 1 - possibleIndex + 1)
      result = Math.min(result, steps)
    }
  }
  
  return result === Infinity ? -1 : result
};







```
