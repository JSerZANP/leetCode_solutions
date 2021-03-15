Youtube video explaining this: https://youtu.be/H1zJFRITZgA

```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function(nums) {
    
    const result = []
    
    for (let i = 0; i < nums.length; i++) {
        let end = i
        while(nums[end + 1] === nums[end] + 1) {
            end += 1
        }
        
        if (end > i) {
            result.push(`${nums[i]}->${nums[end]}`)
        } else {
            result.push(`${nums[i]}`)
        }
        
        i = end
    }
    
    return result
};
```
