A video for this problem: https://youtu.be/9sIvG8x7FKg

```js
const checkPalindromiceAt = (i, j, s, result) => {
  while (i >= 0 && j < s.length && s[i] === s[j]) {
    i--;
    j++;
  }
  if (j - 1 - (i + 1) > result[1] - result[0]) {
    result[0] = i + 1;
    result[1] = j - 1;
  }
};

/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function (s) {
  if (s.length === 0) {
    return "";
  }

  let i = 0;
  const result = [0, 0];
  while (i < s.length) {
    checkPalindromiceAt(i, i, s, result);
    if (i < s.length - 1) {
      checkPalindromiceAt(i, i + 1, s, result);
    }
    i++;
  }

  return s.slice(result[0], result[1] + 1);
};
```
