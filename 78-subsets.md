A video for this problem: https://youtu.be/XbZQigabJeQ

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */

// Time/Space: O(2^n),
var subsets = function(nums) {
    const result = []
    
    const walk = (temp, start) => {
      result.push(temp)
      
      // pick on from the rest, then go on
      for(let i = start; i < nums.length;i++) {
        walk(temp.concat(nums[i]), i + 1)
      }
    }

    walk([], 0)
    return result
};
```
