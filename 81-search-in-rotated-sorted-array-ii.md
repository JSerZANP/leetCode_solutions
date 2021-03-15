A video explaining this: https://youtu.be/Y8DmS7iGggQ

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
// Time: O(logN)
// Space: O(1)
var search = function(nums, target) {
    if(nums.length === 0) return false
  
    // [S1..target..Sk] [Sk+1..middle target.Sn]  1<= k <=n,   S1 >= Sn
    // [12111111]
    let i = 0
    let j = nums.length - 1
    
    while (i <= j) {
      const middle = Math.floor((i + j) / 2)
      
      if (nums[middle] === target) {
        return true
      } else if (target < nums[middle]) {
        // S[j] <= S[i] <= S[middle]
        // S[middle] <= S[j] <= S[i]
        if (nums[middle] > nums[i]) {
          if (target > nums[i]) {
             j = middle - 1
          } else if (target < nums[i]){
            i = middle + 1
          } else {
              return true
          }
        } else if (nums[middle] < nums[i]){
          j = middle - 1
        } else {
          i += 1
        }
      } else {
        // S[j] <= S[i] <= S[middle]
        // S[middle] <= S[j] <= S[i]
        if (nums[middle] > nums[i]) {
          i = middle + 1
        } else if (nums[middle] < nums[i]){
          if (target > nums[j]) {
            j = middle - 1
          } else if (target < nums[j]){
            i = middle + 1
          } else {
              return true
          }
        } else {
           i += 1 
        }
      }
    }
  
    return false
};
```
