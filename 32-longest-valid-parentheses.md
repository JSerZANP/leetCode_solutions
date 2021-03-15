Youtube video explaining this: https://youtu.be/tyLRMPlrvno

```js
/**
 * @param {string} s
 * @return {number}
 */

// Time: O(n)
// Space: O(n)
var longestValidParentheses = function(s) {
    if (s.length === 0) return 0
    // e.g. )()()((
    // XOOOOXXXOOOOOXX
    // ))))(((
  
    // solution is use a stack to track the invalid parenthese index
  
    const stack = []
    let result = 0
    for(let i = 0; i < s.length + 1; i++) {
      if (s[i] === '(') {
        // if they are not matched, then check the substring
        result = Math.max(result, i - (stack.length ? stack[stack.length - 1] : -1) - 1)
        stack.push(i)
      } else {
        // if there is none element in the stack, it is from the beginning
        // get the length of strings to the left side
        if (stack.length === 0) {
          result = Math.max(result, i + 1 - 1)
          stack.push(i)
        } else {
          const topIndex = stack.pop()
          if (s[topIndex] !== '(' || i >= s.length ) {
            // if they are not matched, then check the substring
            result = Math.max(result, i - topIndex - 1)
            stack.push(i)
          }
        }
      }
    }
  
    return result
};
```
