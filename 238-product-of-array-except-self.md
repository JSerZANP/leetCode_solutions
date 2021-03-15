Me explaining it on youtube: https://youtu.be/MljYepMXhAo

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */
var productExceptSelf = function(nums) {
    const result = []
    for (let i = 0; i < nums.length; i++) {
      result[i] = i === 0 ? nums[i] : result[i - 1] * nums[i]
    }
  
    let productRight = 1
    for (let i = nums.length - 1; i > -1; i--) {
      const productLeft = i === 0 ? 1 : result[i - 1]
      result[i] = productLeft * productRight
      
      productRight *= nums[i]
    }
  
    return result
};
```
