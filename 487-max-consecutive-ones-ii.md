My youtube explanation video: https://youtu.be/LaEzdmVkUB0

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(n)
// space: O(1)
var findMaxConsecutiveOnes = function(nums) {
    // 1,0,1,1,0
    //  1,0,0,1, 1, 0
     
     // keep track of prev sub-array-1 length
     // length:             1   2
    //   prev non-1 index:  2   5
  
    let prevNon1Index = -1
    let prevSubArray1Length = 0
    let result = 0
    
    for (let i = 0; i < nums.length + 1; i++) {
      if (nums[i] !== 1) {
        
        const currentSubArray1Length = i - prevNon1Index - 1
        
        
        result = Math.max(result, 
                  currentSubArray1Length +  (nums[prevNon1Index] === 0 ? 1 : 0) + prevSubArray1Length)
        
        prevNon1Index = i
        prevSubArray1Length = currentSubArray1Length
      }
    }
    
    return result
};
```
