A video explaining this: https://youtu.be/ePMcnHsKGN4
```js
/**
 * @param {number} x
 * @return {number}
 */
// TIME: O(n)
// Space: O(1)
var reverse = function(x) {
    let result = 0
    let sign = 1
    
    if (x < 0) {
      sign = -1
      x = -x
    }
  
    while (x > 0) {
      const digit = x % 10
      x = (x - digit) / 10
      result = result * 10 + digit
    }
    
    result *= sign
    
    if (result > 2**31 - 1) return 0
    if (result < -(2**31) - 1) return 0
    
    return result
};
```
