me explaining it on youtube: https://youtu.be/VhqONOjg9go

```js
/**
 * @param {number} num
 * @return {number}
 */


// Time: O(n)
// Space: O(n)
var maximumSwap = function(num) {
    // 2 7 3 6
  
    // 9 2 2 7 3 6
  
    // 9 9 3 7
  
    // from left to right, find the first turning point (desc => asc), i
    // find maximum from i
    // find the first number < maximu, j = 0 -> i
    
    const str = num.toString().split('')
    
    let turningPoint = null
    for (let i = 0; i < str.length - 1; i++) {
      if (str[i] < str[i + 1]) {
        turningPoint = i
        break
      }
    }
    
    if (turningPoint === null) return num
  
    // find the max to the right
    let maxIndexToTheRight = turningPoint + 1
    for (let i = turningPoint + 2; i < str.length; i++) {
      if (str[i] >= str[maxIndexToTheRight]) {
        maxIndexToTheRight = i
      }
    }
  
    // find the first number < maximu
  
    for (let i = 0; i <= turningPoint; i++) {
      if (str[i] < str[maxIndexToTheRight]) {
        // swap
        [str[i], str[maxIndexToTheRight]] = [str[maxIndexToTheRight], str[i]]
        break
      }
    }
  
    return parseInt(str.join(''), 10)
};
```
