Here is a video explaining: https://www.youtube.com/watch?v=h0MTVIgbhH0


```js
/**
 * @param {string} num
 * @return {boolean}
 */
// Time: O(n)
// Space: O(1)
var isStrobogrammatic = function(num) {
    if (num.length === 0) return true
    // 0
    // 1 
    // 1 1
    // 6 9
    // 9 6
    // 8 
    // 8 8
    // 0 0
  
    let i = 0
    let j = num.length - 1
    
    const strogoSingles = new Set(['0', '1','8'])
    const strogoPairs = new Set(['00', '11','69','96','88'])
    
    const isStrobo = (i, j) => {
      if (i === j) {
        return strogoSingles.has(num[i])
      }
      
      return strogoPairs.has(`${num[i]}${num[j]}`)
    }
  
    
    while (i <= j) {
      
      if (!isStrobo(i, j)) {
        return false
      }
      
      i += 1
      j -= 1
    }
  
    return true
};
```
