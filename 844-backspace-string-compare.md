Here is my video explaining : https://youtu.be/ku2EKgqMp0M

```js
/**
 * @param {string} S
 * @param {string} T
 * @return {boolean}
 */

// Time: O(n) n count of the letters
// Space: O(n)
var backspaceCompare = function(S, T) {
    // ab#c
    
    // [a, c]
    
    
    const getTyped = (input) => {
        const result = []
        for (let char of input) {
            if (char === '#') {
                result.pop()
            } else {
                result.push(char)
            }
        }
        return result.join()
    }
    
    return getTyped(S) === getTyped(T)
};
```
