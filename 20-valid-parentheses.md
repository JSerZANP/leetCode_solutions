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

Another try to make the map a bit cleaner

```js
/**
 * @param {string} s
 * @return {boolean}
 */
const pairs = [
  ["(", ")"],
  ["[", "]"],
  ["{", "}"],
];

const map = new Map(pairs);
const reverseMap = new Map(pairs.map(([a, b]) => [b, a]));

var isValid = function (s) {
  const stack = [];
  for (const char of s) {
    if (map.has(char)) {
      stack.push(char);
    } else {
      const top = stack.pop();
      if (top !== reverseMap.get(char)) {
        return false;
      }
    }
  }
  return stack.length === 0;
};
```
