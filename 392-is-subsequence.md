Here is my video explaining it :https://youtu.be/LIpGKvF3Qz0

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */

// two cursors
var isSubsequence = function (s, t) {
  // "abc",  "ahbgdc"

  // abc       a(h)b(gd)c

  let i = 0;
  let j = 0;

  while (i < s.length && j < t.length) {
    if (s[i] === t[j]) {
      i += 1;
      j += 1;
    } else {
      j += 1;
    }
  }

  return i === s.length;
};
```

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isSubsequence = function (s, t) {
  if (s.length === "") return true;

  let i = 0;
  let j = 0;
  while (i < s.length) {
    // for each char in s
    // we try to match one in t
    while (j < t.length && t[j] !== s[i]) {
      j += 1;
    }

    if (j >= t.length) {
      return false;
    }

    i += 1;
    j += 1;
  }

  return true;
};
```
