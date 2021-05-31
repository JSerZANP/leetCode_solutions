video explaining https://www.youtube.com/watch?v=GJvX4qqF5u8

```js
/**
 * @param {number} N
 * @return {boolean}
 */
var reorderedPowerOf2 = function(N) {
    // get permuation, and check if it is power of 2
    
    // length of n
    // n! * log2 N
    
    const normalize = (str) => {
        return str.split('').sort().join('')
    }
    
    const powers = new Set()
    
    const max = 10 ** 9
    
    let base = 1
    while (base <= max) {
        powers.add(normalize(base.toString()))
        base *= 2
    }
    
    return powers.has(normalize(N.toString()))
    
};
```
