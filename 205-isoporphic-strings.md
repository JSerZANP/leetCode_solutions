```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isIsomorphic = function (s, t) {
  if (s.length !== t.length) return false;

  let i = 0;

  const map = new Map();
  const mappedValues = new Set();

  while (i < s.length) {
    if (map.has(s[i])) {
      if (t[i] !== map.get(s[i])) {
        return false;
      }
    } else {
      if (mappedValues.has(t[i])) {
        return false;
      }
      mappedValues.add(t[i]);
      map.set(s[i], t[i]);
    }
    i += 1;
  }
  return true;
};
```
