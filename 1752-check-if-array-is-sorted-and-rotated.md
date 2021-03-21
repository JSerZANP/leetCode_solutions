Here is my explaining video: https://youtu.be/0nhjhVv1VLs
```js
/**
 * @param {number[]} nums
 * @return {boolean}
 */
var check = function(nums) {
    // [a, b][c, d] => [c,d][a,b]
    
    // c -> d
    // a -> b
    // b <= c
    
    // a <= d  => 1
    
    // 1. turning point is maximum 1
    // 2. if has turning point, b <= c
    
    let turningPoints = 0
    for (let i = 1; i < nums.length; i++) {
        if (nums[i] < nums[i - 1]) {
            turningPoints += 1
        }
        
        if (turningPoints > 1) {
            return false
        }
    }
    
    return turningPoints === 0 || nums[nums.length - 1] <= nums[0]
};
```
