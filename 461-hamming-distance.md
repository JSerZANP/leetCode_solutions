Here is my youtube video explaining it : https://youtu.be/X-96S8qg0Hk


```js
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
// Time: O(31) => O(1)
// space: O(1)
var hammingDistance = function(x, y) {
    let result = 0
    
    while (x > 0 || y > 0) {
      const right1 = x % 2
      const right2 = y % 2
      
      if (right1 !== right2) {
        result += 1
      }
      
      x = x >> 1
      y = y >> 1
    }
  
    return result
};
// 0 1 0 0 1 0 1 1 1
// 1 0 0 1 0 1 1 1 1
// 1 1 0 1 1 1 0 0 0   
// 1 1 0 1 1 0 1 1 1   (-1)
// 1 1 0 1 1 0 0 0 0    (&)
// 0 1 0 1
// 0 1 0 0 
// 0 1 0 0 
// 0 0 1 1
// 0
var hammingDistance = function(x, y) {
    let result = 0
    
    let xor = x ^ y
    
    while (xor !== 0) {
      result += 1
      xor = xor & (xor - 1)
    }
  
    return result
};
```
