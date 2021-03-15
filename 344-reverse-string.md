Me explaining this : https://youtu.be/-j0iiF2Qlmo


```js
/**
 * @param {character[]} s
 * @return {void} Do not return anything, modify s in-place instead.
 */

// Time: O(n)
var reverseString = function(s) {
    let start = 0
    let end = s.length - 1
    
    while (start < end) {
      [s[start], s[end]] = [s[end], s[start]]
      start += 1
      end -= 1
    }
  
    return s
};
```
