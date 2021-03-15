Here is my video explaining it: https://youtu.be/9OG4OB6jFso

```js
/**
 * @param {string} s
 * @return {string}
 */
// space: O(26) => O(1) 
// time: O(n * 26z) => O(n)
// 
var removeDuplicateLetters = function(s) {
    // cbacdcbc
    
    // use a Set to keep track of all the letters(unique)
  
    // cbac
    //  bacdc
    //  bacd
    //   acdb
  
    // bcabc
  
    // bca
    // bca
  
    // pre conunt the numbers
    // bca bc
    // a
  
    // [a, b, c] b
  
  
    // OOOOOO
    // ascending  => smllest
    // only chancd we could improve the list, is that is some downward slope
        // i, j ,  S[i] > S[j], and there is another S[i] after S[J]
    // remove these opposite possibilities
    
    
    const countMap = new Map()
    
    for (let char of s) {
      if (countMap.has(char)) {
        countMap.set(char, countMap.get(char) + 1)
      } else {
        countMap.set(char, 1)
      }
    }
    
    const resultStack = []
    const resultSet = new Set()
    
    for (let char of s) {
      if (!resultSet.has(char)) {
        while (resultStack.length > 0) {
          const top = resultStack[resultStack.length - 1]
          if (top < char || countMap.get(top) === 0) {
            break
          }
          
          resultStack.pop()
          resultSet.delete(top)
        }
        
        resultStack.push(char)
        resultSet.add(char)
      }
      countMap.set(char, countMap.get(char) - 1)
    }
  
    return resultStack.join('')
};
```
