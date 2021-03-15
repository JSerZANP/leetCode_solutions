Here is my video explaining this: https://youtu.be/xDhEnt0fjc8

```js
/**
 * @param {number} n
 * @return {number[]}
 */
var grayCode = function(n) {
    // 0 -> 1
    
    // {0, 1}  + (n - 1) case
    
    // 00, 01, 10, 11
    // list(n - 1). reverse(1 + list(n - 1))
    
    
    const result = [0]
    
    for (let i = 1; i <= n; i++) {
        result.push(...result.slice(0).reverse().map(item => item + 2 ** (i - 1)))
    }
    return result
};
```
