Me explaining this on youtube: https://youtu.be/YORTb_6JxYQ

```js
/**
 * @param {string} s
 * @param {number} k
 * @return {number}
 */

// Time: O(2N) => O(n)
// space: O(2) => O(1)
var lengthOfLongestSubstringKDistinct = function(s, k) {
    if (k === 0) return 0
    // eceba
    // eba
  
    // slide window
    // keep track of the occurence with a MAP
    // when add one, and overflowed, remove one from left
    
    const count = new Map()
    let max = 0
    
    let i = 0
    let j = 0
    
    while (j < s.length) {
      const charJ  = s[j]
      
      if (count.has(charJ)) {
        count.set(charJ, count.get(charJ) + 1)
      } else {
        if (count.size === k) {
          // need to remove chars from left
          while (count.size > k - 1) {
            const charI = s[i]
            const countI = count.get(charI)
            if (countI === 1) {
              count.delete(charI)
            } else {
              count.set(charI, countI - 1)
            }
            
            i += 1
          }
        }
        
        // safely add it to hashmap
        count.set(charJ, 1)
      }
      
      max = Math.max(max, j - i + 1)
      j += 1
    }
    
    return max
};
```
