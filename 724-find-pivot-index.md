A video explaining this: https://youtu.be/_Df1OgaqPPg


```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var pivotIndex = function(nums) {
    if (nums.length === 0) return - 1
    if (nums.length === 1) return 1
    
    // get the sum array from left to right
    let sumAll = 0
    for (let i = 0; i < nums.length; i++) {
        sumAll += nums[i]
    }

    let sumLeft = 0
    for (let k = 0; k < nums.length; k++) {
        if (k > 0) {
            sumLeft += nums[k - 1]
        }
        
        if (sumLeft * 2 + nums[k] === sumAll) {
            return k
        }
    }
    return -1
};
```
