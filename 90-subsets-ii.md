Here is a video explaining this: https://youtu.be/cY08iZtNqdI

```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var subsetsWithDup = function(nums) {
    // [a, b, c]
    // pick a number => pick a number from the rest => until there is no number left
    // generate the permupation
    
    // O(nlgn)
    nums.sort()
    
    const result = []
    
    // call stack O(n)
    const pick = (current, start) => {
        result.push(current)
        // [1]
        for (let i = start; i < nums.length; i++) {
            if (i > start && nums[i] === nums[i - 1]) {
                continue
            } else {
                pick(current.concat(nums[i]), i + 1)
            }
        }
    }
    
    // Time: O(2^N)
    pick([], 0)
    
    return result
};
```
