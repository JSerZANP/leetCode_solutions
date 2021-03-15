
A video explaining this: https://youtu.be/pdl569lV1us


```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function(s, t) {
    
    if (s.length !== t.length) {
        return false    
    }
    
    const Occur = new Map()
    
    for (let i = 0; i < s.length; i++) {
        Occur.set(s[i], (Occur.get(s[i]) || 0) + 1)
    }
    
    for (let i = 0; i < t.length; i++) {
        if (!Occur.has(t[i]) || Occur.get(t[i]) === 0) {
            return false
        }
        
        Occur.set(t[i], (Occur.get(t[i]) - 1))
    }
    
    
    for (const [k, v] of Occur) {
        if (v !== 0) {
            return false
        }
    }
    
    return true
};
```
