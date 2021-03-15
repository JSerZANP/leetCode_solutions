A video explaining this: https://youtu.be/y4t6kQ2fSDM

```js
/**
 * @param {number[]} digits
 * @return {number[]}
 */
// Time: O(n)
// Space: O(1)
var plusOne = function(digits) {
    let carryover = 1
    let i = digits.length - 1
  
    while (carryover > 0 && i > -1) {
       
      digits[i] = digits[i] + 1
      if (digits[i] > 9) {
        digits[i] %= 10
        carryover = 1
      } else {
        carryover = 0
      }
      
      i -= 1
    }
  
    // for cases like [9, 9, 9]
    if (carryover > 0) {
      digits.unshift(1)
    }
  
    return digits
};
```
