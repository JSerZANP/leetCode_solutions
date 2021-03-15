Explaining video here: https://youtu.be/tAs9xtMqKwY


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
// Sort first
// var firstMissingPositive = function(nums) {
//     // sort O(n * log(N))
//     const positiveNumbers = nums.filter(i => i > 0)
//     positiveNumbers.sort((a, b) => a - b)
    
//     // [1,1,2]
//     let target = 1
//     for (let i = 0; i < positiveNumbers.length; i++) {
//       if (positiveNumbers[i] === target) {
//         target += 1
//       }
//     }
    
//     return target
// };


// Observervation 
// missing num should <= nums.length + 1

// swap them to where they should be

// [3,4,-1,1,1]
// [-1, 4, 3, 1,1]
// [1, 4, 3, -1,1]
// Time: O(n) + O(n) => O(n)
// Space: O(1)
var firstMissingPositive = function(nums) {
  for (let i = 0; i < nums.length; i++) {
    // if it is not at where it should be
    // and the place for it is not occupied 
    
    // swap current number with the number at is place
    const rightPosition = nums[i] - 1
    if (nums[i] !== i + 1 && rightPosition >= 0 && rightPosition < nums.length && nums[i] !== nums[rightPosition]) {
      const temp  = nums[i]
      nums[i] = nums[rightPosition]
      nums[rightPosition] = temp
      i -= 1
    }
  }
  
  for (let i = 0; i < nums.length; i++) {
     if (nums[i] !== i + 1) {
       return i + 1
     }
  }
  
  return nums.length + 1
};














```
