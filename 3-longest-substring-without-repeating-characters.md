sliding window.

```js
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function (s) {
  if (s.length === 0) return 0;
  // [i, j]
  // keep track of the index.
  const indexMap = new Map();

  // for each step
  // move the right boundary to the right
  // if found the duplicate, move i to that index

  // abcabcbb
  let i = 0; // 1
  let j = 0; // 3
  let result = 0;

  // for each move, it is valid
  while (j < s.length) {
    const char = s[j];
    if (indexMap.has(char)) {
      while (i <= indexMap.get(char)) {
        indexMap.delete(s[i]);
        i += 1;
      }
    }
    indexMap.set(char, j);
    result = Math.max(result, j - i + 1);
    j += 1;
  }

  return result;
};
```
