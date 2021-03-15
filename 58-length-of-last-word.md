A video explaining this: https://youtu.be/ZuvCatYDRyk


```js
/**
 * @param {string} s
 * @return {number}
 */

// state machine
// Time: O(n)
// Space: O(1)
var lengthOfLastWord = function(s) {
    // 'whiteSpace'
    // 'word'
    
    let state = 'whiteSpace'
    let startIndexOfWord = -1
    let lastLength = 0
    
    for (let i = 0; i < s.length + 1; i++) {
      
      // end of word
      if ((s[i] === ' ' || i === s.length) && state !== 'whiteSpace') {
        if (startIndexOfWord > -1) {
          lastLength = i - startIndexOfWord
        }
        state = 'whiteSpace'
      }
      
      // start of word
      if (s[i] !== ' ' && state !== 'word') {
        startIndexOfWord = i
        state = 'word'
      }
        
    }
  
    return lastLength
};
```
