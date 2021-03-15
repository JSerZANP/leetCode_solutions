Me explaining this on youtube: https://youtu.be/YMSCmC-srzc
```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */

// Time: O(n)
// space: O(1)
var missingElement = function(nums, k) {
    // loop through the element, and find the diff
    // if diff is enough, return result
    // if not, continue
    
    nums.push(Infinity)
    
    for (let i = 1; i < nums.length; i++) {
        const diff = nums[i] - nums[i - 1]
        if (diff - 1 >= k) {
            return nums[i - 1] + k
        } else {
            k -= diff - 1
        }
    }

};
```
