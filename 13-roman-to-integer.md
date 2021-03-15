A video explaining this: https://youtu.be/fE3vsgt2bC8

```js
const map = {
  'I': 1,
  'V': 5,
  'X': 10,
  'L': 50,
  'C': 100,
  'D': 500,
  'M': 1000
}


/**
 * @param {string} s
 * @return {number}
 */
var romanToInt = function(s) {
    let sum = 0
    
    for (let i = 0; i < s.length; i++) {
      let sign = 1
      if (i < s.length - 1 && (map[s[i + 1]] === map[s[i]] * 5 || map[s[i + 1]] === map[s[i]] * 10)) {
        sign *= -1
      }
      
      sum += sign *  map[s[i]]
    }
  
    return sum
};
```
