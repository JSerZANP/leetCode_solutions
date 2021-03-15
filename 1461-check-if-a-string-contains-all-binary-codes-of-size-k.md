Here is me explaining it: https://youtu.be/Pd_N0MKdQtQ
```js
/**
 * @param {string} s
 * @param {number} k
 * @return {boolean}
 */

// Time: O(nk)
// Space: O(2^k)
var hasAllCodes = function(s, k) {
    // brute force
    // O(2^k * n)
  
    // get all substrings (Set) then check existence by O(1)
    // check Set.size O(1)
  
    const substrings = new Set()
    
    for (let i = 0; i + k - 1 < s.length; i++) {
      substrings.add(s.slice(i, i + k - 1 + 1))
    }
  
    return substrings.size === 2 ** k
};
```
