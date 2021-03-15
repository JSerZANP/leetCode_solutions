Here is a video explaining this: https://youtu.be/XQR0KeyVciM

```js
/**
 * @param {string} s
 * @return {string[]}
 */
var restoreIpAddresses = function(s) {
    // 0.0.0.0 ~ 255.255.255.255
    const result = []
    
    
    const walk = (temp, countOfSegments, start) => {
        if (countOfSegments === 4 && start === s.length) {
            result.push(temp)
        }
        
        if (countOfSegments < 4) {
            for (let i = start; i < start + 3 && i < s.length; i++) {
                const num = s.slice(start, i + 1)
                if (num <= 255) {
                    walk(temp + (temp === '' ? '' : '.') + num, countOfSegments + 1, i + 1)
                    if (num == 0) break
                } else {
                    break
                }
            }
        }
    }
    
    walk('', 0, 0)
    
    return result
};
```
