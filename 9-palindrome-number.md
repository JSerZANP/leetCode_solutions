A video explaining this: https://youtu.be/Apz80J3ONVY

```js
/**
 * @param {number} x
 * @return {boolean}
 */

// TIME: log10(x)
// Space: O(1)

// by comparing the first and last digit
// var isPalindrome = function(x) {
//     if (x < 0) return false
    
//     // get the length of digits
//     let length = 1
//     let base = 1
//     while (base * 10 <= x) {
//       length += 1
//       base *= 10
//     }

//     while (base > 1) { 
//       // first digit
//       const firstDigit = Math.floor(x / base)
//       const lastDigit = x % 10
      
//       if (firstDigit !== lastDigit) {
//         return false
//       }
      
//       x = Math.floor((x - base * firstDigit) / 10)
      
//       base = base / 100
//     }
  
//     return true
// };

// TIME: log10(x)
// Space: O(1)
// calculate the reversed number
var isPalindrome = function(x) {
    if (x < 0) return false
    
    // get the last digits accumulatively
    // and sum up
    let reversedNumber = 0
    const originalX = x
    
    while (x > 0) {
      const digit = x % 10
      reversedNumber = reversedNumber * 10 + digit
      x = (x - digit) / 10
    }
    return reversedNumber === originalX
};
```
