A video explaining this: https://youtu.be/nagl6LE62xg

```js
/**
 * @param {string} s
 * @return {boolean}
 */

// TIME: O(n)
// Space: O(n)

var isValid = function (s) {
  const pair = {
    "]": "[",
    ")": "(",
    "}": "{",
  };

  const stack = [];

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (["(", "[", "{"].includes(char)) {
      stack.push(char);
    } else {
      const top = stack.pop();
      if (top !== pair[char]) {
        return false;
      }
    }
  }

  return stack.length === 0;
};
```
