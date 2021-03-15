Here is my youtube explanation: https://youtu.be/Fj24xroI-S4
```js
/**
 * @param {string} word
 * @return {boolean}
 */
var detectCapitalUse = function(word) {
  // if lower case char: invalid case is prev is upper case & not the first letter
  // if upper case: if have lower case before it, invalid
  
  let hasUpper = false
  let hasLower = false
  
  for (let i = 0, total = word.length; i < total; i++) {
    if (/[a-z]/.test(word[i])) {
      if (hasUpper && !hasLower && i > 1) {
        return false
      }
      
      hasLower = true
    } else {
      if (hasLower) {
        return false
      }
      hasUpper = true
    }
  }
  
  return true
};
```
