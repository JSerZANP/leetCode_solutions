A video explaining this: https://youtu.be/yTB92FXcopc

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function(s, p) {
    const check = (s, p, i, j) => {
      // aaa vs a*a*a*a*
      if (j > p.length - 1) {
        return i > s.length - 1
      }
      
      const isNextQuantiyModifier = p[j + 1] === '*'
      
      if (!isNextQuantiyModifier) {
        if ([s[i], '.'].includes(p[j])) {
          return i < s.length && check(s, p, i + 1, j + 1)
        } else {
          return false
        }
      } else {
        // aa vs a*, finally 2 vs 0
        if ([s[i], '.'].includes(p[j])) {
          return check(s, p, i, j + 2) || (i < s.length && check(s, p, i + 1, j))
        } else {
          return check(s, p, i, j + 2)
        }
      }
      
    }
    
    return check(s, p, 0, 0)
};
```
