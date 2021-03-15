A video explaining this: https://youtu.be/gdgx4HHBmKg

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var subarraySum = function(nums, k) {
    let result = 0
    const countMap = new Map([[0, 1]])
    
    let sum = 0
    
    for (let num of nums) {
      sum += num
      
      if (countMap.has(sum - k)) {
        result += countMap.get(sum - k)
      }
      
      if (countMap.has(sum)) {
        countMap.set(sum, countMap.get(sum) + 1)
      } else {
        countMap.set(sum, 1)
      }
    }
  
    return result
};
```
