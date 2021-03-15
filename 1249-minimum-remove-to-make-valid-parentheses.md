Here is my video of explaining it on youtube: https://youtu.be/TvAVIJnfmVA

```js
const minRemoveToMakeValid = (s) => {
  // two way parse
  let countOfLeft = 0
  let countOfRight = 0
  let resultFor1Pass = ''
  
  for (let i = 0; i < s.length; i++) {
    if (s[i] === '(') {
      countOfLeft += 1
    } else if (s[i] === ')') {
      if (countOfRight === countOfLeft) {
        continue
      }
      countOfRight += 1
    }
    resultFor1Pass += s[i]
  }
  
  // when it is done, extra left parentheses are to be removed
  let extraLeftParenCount = countOfLeft - countOfRight
  
  if (extraLeftParenCount === 0) return resultFor1Pass
  
  let result = ''
  
  for (let j = resultFor1Pass.length - 1; j > -1 ; j--) {
    if (resultFor1Pass[j] === '(') {
      extraLeftParenCount -= 1
      
      if (extraLeftParenCount === 0) {
        result = resultFor1Pass.slice(0, j) + result
        break
      }
    } else {
      result = resultFor1Pass[j] + result
    }
  
  }
  
  return result
}
```
