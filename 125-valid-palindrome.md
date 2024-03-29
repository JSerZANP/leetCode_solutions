A video explaining this: https://youtu.be/AB1r7Xf7lVU

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var isPalindrome = function (s) {
  if (s.length === 0) return true;
  const regAlphanumeric = /[0-9a-zA-Z]/;

  let i = 0;
  let j = s.length - 1;

  while (i < j) {
    while (!regAlphanumeric.test(s[i]) && i < s.length - 1) {
      i += 1;
    }

    while (!regAlphanumeric.test(s[j]) && j > 0) {
      j -= 1;
    }

    if (i >= j) return true;

    if (s[i].toLowerCase() !== s[j].toLowerCase()) return false;

    i += 1;
    j -= 1;
  }

  return true;
};
```
