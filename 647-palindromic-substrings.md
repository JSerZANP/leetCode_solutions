Here is my youtube video explaining this: https://youtu.be/fG0bZx1s-74

```js
/**
 * @param {string} s
 * @return {number}
 */

// Time: O(n^2)
// sapce: O(1)
var countSubstrings = function(s) {
    // abccba => true O(n)
    // n^2 substring
    // O(n^3)
    
    // abccba > bccb > cc
    // a  0
    // ab 0.5
    // b  abc 1
    
    // O(2n * n) 
    
    // 1. fix the center and expand to all the sub string
    
    
    let result = 0
    
    for (let center = 0; center < s.length; center += 0.5) {
        let left = Math.floor(center)
        let right = Math.ceil(center)
        
        while (left >= 0 && right < s.length) {
            
            if (s[left] === s[right]) {
                result += 1
            } else {
                break
            }
            
            left -= 1
            right += 1
        }
    }
    
    return result
};
```
