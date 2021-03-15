Here is my explanation on youtube: https://youtu.be/IXXPT9kmf0g

```js
/**
 * @param {string} S
 * @return {string}
 */
var removeDuplicates = function(S) {
    const stack = []
    
    for (let i = 0; i < S.length; i++) {
        if (stack[stack.length - 1] === S[i]) {
            stack.pop()
        } else {
            stack.push(S[i])
        }
    }
    
    return stack.join('')
};
```
