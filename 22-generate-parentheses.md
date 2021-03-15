A video explaining this: https://youtu.be/Tna92fSOQTs

```js
/**
 * @param {number} n
 * @return {string[]}
 */

/*

1. ()

2. ()()   (())

3 =  1 + 2
  =  2 + 1
  =  3 + 0
*/

// Recursion
// Time: f(n) = f(n - 1)* f(0) + f(n -2) * f(1) + f(n-3) * f(2) ?
// var generateParenthesis = function(n) {
//     if (n === 0) {
//       return ['']
//     }
  
//     if (n === 1) {
//       return ['()']
//     }
    
//     const result = []
//     for (let i = 1; i <= n; i++) {
//       const leftInner = generateParenthesis(i - 1)
//       const right = generateParenthesis(n - i)
      
//       leftInner.forEach(itemLeft => {
//         right.forEach(itemRight => {
//           result.push(`(${itemLeft})${itemRight}`)
//         })
//       })
//     }
  
//     return result
// };


// Iteration
var generateParenthesis = function(n) {
    const results = [[''], ['()']]
    
    for (let i = 2; i <=n; i++) {
      const result = []
      for (let j = 1; j <= i; j++) {
        const leftInner = results[j - 1]
        const right = results[i - j]
        leftInner.forEach(itemLeft => {
          right.forEach(itemRight => {
            result.push(`(${itemLeft})${itemRight}`)
          })
        })
      }
      results[i] = result
    }
  
    return results[n]
};
```
