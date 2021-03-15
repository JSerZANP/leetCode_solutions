Youtube video explaining this: https://youtu.be/wM_PMOwlufc


```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
    const match = (i, j) => {
      if (i >= s.length && j >= p.length) {
        return 0
      }
      // adasdasd aa  dsadasd aa dd ba  dd a asdfas  bbaa
      // *        aa    *      ba  *  a     *   bb
      if (i < s.length && (s[i] === p[j] || p[j] === '?')) {
        return match(i + 1, j + 1)
      } else if (p[j] === '*') {
        // skip the sequential *
        while (p[j + 1] === '*') {
          j += 1
        }
        
        for(let k = i; k <= s.length;k++) {
          const result = match(k, j + 1)
          if (result === 0) {
            return 0
          } else if (result === 1) {
            break 
          }
        }
        
        return 1
      }
      
      return -1
    }
    
    return match(0, 0) === 0
};
```
