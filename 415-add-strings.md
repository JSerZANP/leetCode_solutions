Here is my video of explaining it: https://youtu.be/SZKe-EwXB68
```js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */
var addStrings = function(num1, num2) {
  const length1 = num1.length
  const length2 = num2.length
  
  const maxLength = Math.max(length1, length2)
  const resultArr = new Array().fill(0)
  
  let carry = 0
  // from right to left
  for (let i = 0; i < maxLength; i++) {
    const digit1 = (num1[length1 - 1 - i] || 0) - 0
    const digit2 = (num2[length2 - 1 - i] || 0) - 0
    
    let sum = digit1 + digit2 + carry
    if (sum > 9) {
      sum -= 10
      carry = 1
    } else {
      carry = 0
    }
    
     resultArr[maxLength - 1 - i] = sum
  }
  let resultStr = resultArr.join('')
  return carry > 0 ? '1' + resultStr : resultStr
};
```
