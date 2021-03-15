Here is a video explaining this: https://youtu.be/g9RECnfohLE


```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(n^2)
// space: O(n)
// var lengthOfLIS = function(nums) {
//   if (nums.length === 0) return 0
//   // 10,9,2,5,3,7,101,18
  
//   // optimal subarray, if 18 is in it
//   // LIS(i)
//   // LISEnd(I) is the longest incresing subarray length which end at i
  
//   // LISEND(i) = max { 
//   //        LISTEND(j) + 1, j = 0 -> i - 1, if (nums[i] > nums[j])
//   //        -Infinity
//   // }
  
  
//   // LIS(i) = max { LISEND(I) }  i = 0 -> nums.length - 1
  
//   let result = 1
  
//   const LISEndAt = new Array(nums.length).fill(1)
  
//   for (let i = 1; i < nums.length; i++) {
//     LISEndAt[i] = Math.max(
//       1,
//       ...LISEndAt.slice(0, i).map((item, j) => {
//         return nums[i] > nums[j] ? item + 1 : 0
//       })
//     )
    
//     result = Math.max(LISEndAt[i], result)
//   }
//   return result
// }

var lengthOfLIS = function(nums) {
  if (nums.length === 0) return 0
  // 10,9,2,5,3,7,101,18, 4, 19, 5 6 7,8
  
  // 2 3 4 5 6 7 
  // 2 3 4 5 6
  // 2 3 4 5 
  // 2 3 4
  // 2 3
  // 2
  
  //  2   10   11  5
  
  // 2 
  // 2 5
  // 2 10 11
  
  // shorter optimozal subarray has a smaller ending
  
  // use a array to hold ending item at optimal subarray with length i
  const endings = [0, nums[0]]
  
  numLoop: for (let i = 1;  i < nums.length; i++) {
    // binary search the right optimal length
    // binary search the insert position
    const num = nums[i]
    let start = 1
    let end = endings.length - 1
    
    while (start <= end) {
        const middle = Math.floor((start + end) / 2)
        if (endings[middle] === num) continue numLoop
        
        if (endings[middle] > num) {
          end = middle - 1
        } else {
          start = middle + 1
        }
    }
    // start is the inserting position index
    // start means the length of the optimal
    const lengthOfOptimalSubArray = start
    if (endings[lengthOfOptimalSubArray] === undefined) {
      endings[lengthOfOptimalSubArray] = num
    } else {
      endings[lengthOfOptimalSubArray] = Math.min(endings[lengthOfOptimalSubArray], num)
    }
  }
  return endings.length - 1
}


```
