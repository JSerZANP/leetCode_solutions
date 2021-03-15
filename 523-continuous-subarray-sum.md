Watch my video for explanation: https://youtu.be/9DMEGpnmIMM

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {boolean}
 */
// var checkSubarraySum = function(nums, k) {
//     // brute force
//     // n^2 * n = O(n ^ 3)
//     // O(1)
  
  
//     // improve to O(n ^ 2
//     for (let i = 0; i < nums.length - 1; i++) {
//       let sum = nums[i]
//       for (let j = i + 1; j < nums.length; j++) {
//         sum += nums[j]
//         const mod = k === 0 ? sum : sum % k
//         if (mod === 0) {
//           return true
//         }
//       }
//     }
    
//     return false
// };


// Time : O(n)
// space: worst is k === 0, and the last two numbers being 0
// O(n)
// O(k - 1) if k !== 0
var checkSubarraySum = function(nums, k) {
    // 23, 2, 4, 6, 7
    // 5, 2, 4, 0, 1
    // 5, 1, 5
  
    // 0 2 3 1 5
    // 0 2 5 0 5
  
    const mods = new Map() // Map<mod, index>
  
    let sum = 0
    for (let i = 0; i < nums.length; i++) {
      sum += nums[i]
      
      if (k !== 0) {
        sum %= k
      }
      
      // if sum is 0, then all are 0
      // only invalid case one 0, so we filter this one case out
      if (sum === 0 && i > 0) {
        return true
      }
      
      if (mods.has(sum)) {
        if (mods.get(sum) < i - 1) {
          return true
        }
      } else {
        mods.set(sum, i)
      }
    }
  
    return false
};



```
