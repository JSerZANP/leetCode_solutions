My video explaining this: https://youtu.be/bk1NdxowB6M

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// DP
// Time: O(n)
// Space: O(n)
// var maxSubArray = function(nums) {
//     // f(n) means maximum subarray ending at index n
  
//     // f(n) === Math.max(f(n - 1) + nums[n], nums[n])
  
//     // maximun = Math.max(f(n))
  
//     let maxes = Array(nums.length).fill(Number.NEGATIVE_INFINITY)
//     maxes[0] = nums[0]
//     let maximum = nums[0]
  
  
//     for (let i = 1; i < nums.length; i++) {
//       if (maxes[i - 1] <= 0) {
//         maxes[i] = nums[i]
//       } else {
//         maxes[i] = maxes[i - 1] + nums[i]
//       }
      
//       maximum = Math.max(maximum, maxes[i])
//     }
  
//     return maximum
// };


// Divide and conquer

var maxSubArray = function(nums) {
    const max = (i, j) => {
      if (i === j) return nums[i]
      
      const middle = Math.floor((i + j) / 2)
      
      let maxLeft = nums[middle]
      let sumLeft = nums[middle]
      for (let k = middle - 1; k > -1 ; k--){
        sumLeft += nums[k]
        maxLeft = Math.max(sumLeft, maxLeft)
      }
      
      let maxRight = nums[middle + 1]
      let sumRight = nums[middle + 1]
      for (let k = middle + 2; k < nums.length ; k++){
        sumRight += nums[k]
        maxRight = Math.max(sumRight, maxRight)
      }
      
      return Math.max(maxLeft + maxRight, max(i, middle), max(middle + 1, j))
    }
    
    return max(0, nums.length - 1)
};
```
