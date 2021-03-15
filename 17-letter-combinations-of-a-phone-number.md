A video explaning this: https://youtu.be/ycyGl4dynDw

```js
/**
 * @param {string} digits
 * @return {string[]}
 */

// Recursion
// Time: O(3^n)
// Space: O(3^N) + O(N)
// var letterCombinations = function(digits) {
//     const map = {
//       1: [],
//       2: ['a','b','c'],
//       3: ['d', 'e', 'f'],
//       4: ['g', 'h', 'i'],
//       5: ['j', 'k', 'l'],
//       6: ['m', 'n', 'o'],
//       7: ['p', 'q', 'r', 's'],
//       8: ['t', 'u', 'v'],
//       9: ['w', 'x', 'y', 'z']
//     }
    
//     const result = []
    
//     // walk throught the digits, with temporary result(prefix) on our back
//     const walk = (i, prefix) => {
//       if (i > digits.length - 1) {
//         result.push(prefix)
//         return
//       }
      
//       const digit = digits[i]
//       for (let char of map[digit]) {
//         walk(i + 1, prefix + char)
//       }
//     }
    
//     if (digits.length > 0) {
//       walk(0, '')
//     }
  
//     return result
// };


// Iteration (BFS)
var letterCombinations = function(digits) {
    if (digits.length === 0) return []
    const map = {
      1: [],
      2: ['a','b','c'],
      3: ['d', 'e', 'f'],
      4: ['g', 'h', 'i'],
      5: ['j', 'k', 'l'],
      6: ['m', 'n', 'o'],
      7: ['p', 'q', 'r', 's'],
      8: ['t', 'u', 'v'],
      9: ['w', 'x', 'y', 'z']
    }
    
    const result = ['']
    
    for (let i = 0; i < digits.length; i++) {
      const digit = digits[i]
      
      result.push(null)
      let head
      while ((head = result.shift()) !== null) {
        for (let char of map[digit]) {
          result.push(head + char)
        }
      }
    }
  
    return result
};




```
