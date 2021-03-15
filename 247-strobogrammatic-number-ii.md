Me explaining it on youtube: https://youtu.be/THMY52gMtdo

```js
/**
 * @param {number} n
 * @return {string[]}
 */

// Time: An = An-2 * 5 => 5^n
// space: O(1)
var findStrobogrammatic = function(n) {
    if (n === 0) return []
    // 0
    // 1
    // 6 - 9
    // 8
    // 0 0
    // 1 1 
    // 8 8 
    // 9 - 6
  
    // 0 1 8  => singles
    // 0 0 , 1 1, 8 8, 6 9, 9 6 => pairs
    
    
    // if n is 1 => singles
    // if n is 2 => pairs
    // if n is odd, put each pair to combinations at n - 2
  
    const singles = ['0', '1', '8']
    const pairs = ['00', '11', '88', '69', '96']
    
    let result = n % 2 === 1 ? singles.slice(0) : ['']
    
    let length = n % 2 === 1 ? 1 : 0
    
    while (length < n) {
      // push the pairs in to the current combinations
      const appended = []
      for (let combination of result) {
        for (let pair of pairs) {
          if (pair === '00' && length + 2 === n) continue
          appended.push(pair[0] + combination + pair[1])
        }
      }
      result = appended
      length += 2
    }
  
    return result
};
```
