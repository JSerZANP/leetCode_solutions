A video explaining this: https://youtu.be/pdl569lV1us

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isAnagram = function (s, t) {
  if (s.length !== t.length) {
    return false;
  }

  const Occur = new Map();

  for (let i = 0; i < s.length; i++) {
    Occur.set(s[i], (Occur.get(s[i]) || 0) + 1);
  }

  for (let i = 0; i < t.length; i++) {
    if (!Occur.has(t[i]) || Occur.get(t[i]) === 0) {
      return false;
    }

    Occur.set(t[i], Occur.get(t[i]) - 1);
  }

  for (const [k, v] of Occur) {
    if (v !== 0) {
      return false;
    }
  }

  return true;
};
```

Another try

```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
const charCodeA = "a".charCodeAt(0);
var isAnagram = function (s, t) {
  if (s.length !== t.length) return false;

  const occurances1 = new Array(26).fill(0);
  const occurances2 = new Array(26).fill(0);

  for (const char of s) {
    const index = char.charCodeAt(0) - charCodeA;
    occurances1[index] += 1;
  }

  for (const char of t) {
    const index = char.charCodeAt(0) - charCodeA;
    occurances2[index] += 1;

    if (occurances2[index] > occurances1[index]) {
      return false;
    }
  }

  for (const index of occurances1) {
    if (occurances1[index] !== occurances2[index]) {
      return false;
    }
  }

  return true;
};
```
