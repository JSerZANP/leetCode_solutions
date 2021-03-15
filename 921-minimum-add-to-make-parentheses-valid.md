Here is my video explaining it: https://youtu.be/Bzzu4vAozYA

```js
/**
 * @param {string} S
 * @return {number}
 */

// Time: O(n)
// Space: O(1)
var minAddToMakeValid = function(S) {
    let invalidLeftCount = 0
    let invalidRightCount = 0
    
    for (let char of S) {
      if (char === '(') {
        invalidLeftCount += 1 
      } else {
        if (invalidLeftCount === 0) {
          invalidRightCount += 1
        } else {
          invalidLeftCount -= 1 
        }
      }
    }
  
    return invalidLeftCount + invalidRightCount
};
```
