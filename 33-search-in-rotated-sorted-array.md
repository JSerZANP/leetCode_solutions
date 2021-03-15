A video explaining this: https://youtu.be/4phx7g8QXVM

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
// Time: O(logN)
// Space: O(1)
var search = function(nums, target) {
    if(nums.length === 0) return -1
  
    // [S1...Sk] [Sk+1...Sn]  1<= k <=n,   S1 > Sn
    let i = 0
    let j = nums.length - 1
    
    while (i <= j) {
      const middle = Math.floor((i + j) / 2)
      
      if (nums[middle] === target) {
        return middle
      } else if (target < nums[middle]) {
        // S[j] < S[i] <= S[middle]
        // S[middle] <= S[j] < S[i]
        if (nums[middle] >= nums[i]) {
          if (target >= nums[i]) {
             j = middle - 1
          } else {
            i = middle + 1
          }
        } else {
          j = middle - 1
        }
      } else {
        // S[j] < S[i] <= S[middle]
        // S[middle] <= S[j] < S[i]
        if (nums[middle] >= nums[i]) {
          i = middle + 1
        } else {
          if (target > nums[j]) {
            j = middle - 1
          } else {
            i = middle + 1
          }
        }
      }
    }
  
    return -1
};
```
