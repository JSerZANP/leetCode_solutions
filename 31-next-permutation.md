
A video explaining this: https://youtu.be/eV5K3TDNdRs

```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */

// Time: O(n)
// Space: O(1)
// var nextPermutation = function(nums) {
//     if (nums.length < 2) return nums
//     // 1 2 5 1 4 => 1 2 5 4 1
  
//     // 1 2 5 4 1 => 1 4 1 2 5
  
//     //  1 1 2 4 5   asc
//     //  5 4 2 1 1   desc
//     // right to left
  
//     /*   
//           5
//                1
//       2  
//     1        4
  
  
  
//     5 5
//         4
//            2
//              1  1
             
             
//     5 4  2 1 1
//     1 4 2 1 5
//     1 1 2 4 5
    
//      solution:
//       from right to left, find the first descing slope, get bottom next to peak => x, y
//       from right to left, find the first number bigger than x => z
//       swap x <-> z
//       sort numbers from right to y
//     */
  
//    // 10 2 4 3 1 ==>  10 3 4 2 1 =>  10 3 1 2 4
//     let rightMostPeak
//     // O(n)
//     for (let i = nums.length - 1; i > -1; i--) {
//       if (i === 0) {
//         rightMostPeak = 0
//       }
      
//       // if peak found
//       if (nums[i - 1] < nums[i]) {
//         rightMostPeak = i
//         break
//       }
//     }
  
//     // now find the first number bigger than the bottom number
//      // and swap with bottom number
//     // if no bottom, skip
//   // O(n)
//     if (rightMostPeak > 0) {
//       for (let i = nums.length - 1; i > -1; i--) {
//         if (nums[i] > nums[rightMostPeak - 1]) {
//           [nums[i], nums[rightMostPeak - 1]] = [nums[rightMostPeak - 1], nums[i]] 
//           break;
//         }
//       }
//     }
  
//     // use two cursor to do inline reversing of the numbers from right to the peak
  
//     let j = rightMostPeak
//     let k = nums.length - 1
//     // O(n)
//     while (j < k) {
//       [nums[j], nums[k]] = [nums[k], nums[j]] 
//       j += 1
//       k -= 1
//     }
    
//     return nums
// };


var nextPermutation = function(nums) {
  if (nums.length < 2) return
  
  // 1. find the first turning point from right, left most one.  the one to the left is the target to swap
  
  let turningPoint = null
  for (let i = nums.length - 1; i > 0; i--) {
    if (nums[i] > nums[i - 1]) {
      turningPoint = i
      break
    }
  }
  
  if (turningPoint === null) {
    nums.reverse()
    return
  }
  
  // 2. find the first number bigger than swap target from right. swap
  
  const targetIndex = turningPoint - 1
  
  for (let i = nums.length - 1; i >= turningPoint; i--) {
    if (nums[i] > nums[targetIndex]) {
      [nums[i], nums[targetIndex]] = [nums[targetIndex], nums[i]]
      break
    }  
  }
  
  // 3. reverse the order from right till the turning point
  
  let start = turningPoint
  let end = nums.length - 1
  
  while (start < end) {
    [nums[start], nums[end]] = [nums[end], nums[start]]
    start += 1
    end -= 1
  }
  
  return
}
```
