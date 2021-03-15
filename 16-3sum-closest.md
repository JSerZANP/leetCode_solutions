A video explaining this: https://youtu.be/C2mT-EgNwMk
```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var threeSumClosest = function(nums, target) {
  let result = Number.POSITIVE_INFINITY


  // sort the nums O(lgN)
  nums.sort((a, b) => a - b)


  // [-4, -1, -1, 0, 1, 2]

  // n * n , total + O(n^2) => O(n^2)
  // Space: 3Cn

  for (let i = 0; i < nums.length - 2; i++) {
    // fix ith number as left one
    let j = i + 1
    let k = nums.length - 1

    while (j < k) {
      const sum = nums[i] + nums[j] + nums[k]
      
      const currentDelta = sum - target
      
      if (currentDelta === 0) return target
      
      if (currentDelta < 0) {
          // move to the next different number
          j += 1
          while (nums[j] === nums[j - 1]) {
            j += 1
          }
      }

      if (currentDelta > 0) {
          // move to the next different number
          k -= 1
          while (nums[k] === nums[k + 1]) {
            k -= 1
          }
      }
      if (Math.abs(currentDelta) < Math.abs(result - target)) {
        result = sum
      }
    }

    // move to the next different number
    while (nums[i + 1] === nums[i]) {
      i += 1
    }
  }

  return result
};
```
