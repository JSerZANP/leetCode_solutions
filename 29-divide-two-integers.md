A video explaining this: https://youtu.be/NoL6TMwUGuw


```js
/**
 * @param {number} dividend
 * @param {number} divisor
 * @return {number}
 */
// naive approach, keep doing substraction
// O(n/m)
// var divide = function(dividend, divisor) {
//     let sign = 1
//     if ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0)) {
//       sign = -1
//     }
//     dividend = Math.abs(dividend)
//     divisor = Math.abs(divisor)
//     let result = 0
//     while (dividend >= divisor) {
//       dividend -= divisor
//       result += 1
//     }
    
//     return Math.min(Math.max(result * sign, -(2 ** 31)), 2**31 - 1)
// };

//  improvement
//  22 / 3
//  1 2 4
//  3 6 12 24  ..... by adding  3 x 2**n
// 22 - 12 => 10   +4
//  10 - 6 => 4   +2
//  4 - 3 => 1   + 1

var divide = function(dividend, divisor) {
  
    let sign = 1
    if ((dividend > 0 && divisor < 0) || (dividend < 0 && divisor > 0)) {
      sign = -1
    }
  
    dividend = Math.abs(dividend)
    divisor = Math.abs(divisor)
  
    const baseOn2 = []
    const baseOnDivisor = []
    
    let i = 1
    let j = divisor
    while (j <= dividend) {
      baseOn2.push(i)
      baseOnDivisor.push(j)
      
      i += i
      j += j
    }
  
    // collect the result
    let result = 0
    for (let k = baseOnDivisor.length - 1; k > -1; k--) {
      if (dividend >= baseOnDivisor[k]) {
        result += baseOn2[k]
        dividend -= baseOnDivisor[k]
      }
    }
    
    return Math.min(Math.max(result * sign, -(2 ** 31)), 2**31 - 1)
};
```
