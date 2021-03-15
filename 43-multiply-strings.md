A video explaining this: https://youtu.be/TFlv8yZBtDo

```js
/**
 * @param {string} num1
 * @param {string} num2
 * @return {string}
 */

// Time: O(n * m)
// Space: O(n + m)
var multiply = function(num1, num2) {
  const result = Array(num1.length + num2.length).fill(0)
  
  for (let j = num2.length - 1; j > -1; j--) {
    for (let i = num1.length - 1; i > -1; i--) {
      const product = num1[i] * num2[j]
      const index = num1.length + num2.length - 1 - (num2.length - 1 - j + num1.length - 1 - i)
      result[index] += product
      if (result[index] > 9) {
        result[index - 1] += Math.floor(result[index] / 10)
        result[index] %= 10
      }
    }
  }

  // 99 * 9 => carry digit
  // 11 * 1 => no carry digt
  // skip the leading zeros
  while (result[0] === 0) {
    result.shift()
  }
  
  return result.length === 0 ? '0' : result.join('')
};
```
