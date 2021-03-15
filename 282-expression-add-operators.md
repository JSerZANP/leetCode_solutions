me explaining this on youtube: https://youtu.be/9SQ1tZYP9Vs


```js
/**
 * @param {string} num
 * @param {number} target
 * @return {string[]}
 */
var addOperators = function(num, target) {
    // brute force
    // O(4 ^ (n - 1) * n)
    
  
    // (+) 1 2 3
    // 1 + 2 (sum)
    // 1 - 2 (sum, next * -1)
    // 1 * 2 (sum, next * 1)
  
    // 2 + 3 +    sum = 2,  next head number * 1
    // 2 - 3 -    sum = 2,  next head number * -1
    // 2 * 3 *     sum = 0,  next head numer * 2
    const possibilities = []
    
    const walk = (start, toSum, toMultiply, temp) => {
      // TODO: check the ending condition
      // operator next to i
      for (let i = start; i < num.length; i++) {
        // if num[start] is 0, it should be 0 itself, 00, 01 are invalid
        if (num[start] === '0' && i > start) {
          break
        }
        
        const headStr = num.slice(start, i + 1)
        
        const headNum = parseInt(headStr, 10)
        
        const result = headNum * toMultiply + toSum
        
        const prefix = temp + headStr
        if (i === num.length - 1) {
          if (result === target) {
            possibilities.push(prefix)
          }
        } else {
            // case '+'
          walk(i + 1, result, 1, prefix + '+')

          // case '-'
          walk(i + 1, result, -1, prefix + '-')

          // case '*'
          walk(i + 1, toSum, toMultiply * headNum, prefix + '*')
        }
      }
    }
    
    walk(0, 0, 1, '')
  
    return possibilities
};
```
