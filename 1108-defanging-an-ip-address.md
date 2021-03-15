me explaining this on youtube: https://youtu.be/kXYdQ3SHAx0


```js
/**
 * @param {string} address
 * @return {string}
 */
// var defangIPaddr = function(address) {
//     return address.replace(/\./g, '[.]')
// };

// Time: O(n)
// var defangIPaddr = function(address) {
//     return address.split('.').join('[.]')
// };


// Time: O(n)
// Space: O(1)
var defangIPaddr = function(address) {
    let result = ''
    let prevDotIndex = -1
    for (let i = 0; i < address.length + 1; i++) {
        if (i === address.length) {
            result += address.slice(prevDotIndex + 1, i)
        } else if (address[i] === '.') {
            result += address.slice(prevDotIndex + 1, i)
            result += '[.]'
            prevDotIndex = i
        }
    }
    return result
};
```
