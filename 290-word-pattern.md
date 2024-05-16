```js
/**
 * @param {string} pattern
 * @param {string} s
 * @return {boolean}
 */
var wordPattern = function (pattern, s) {
  const words = s.split(" ");
  const chars = pattern.split("");
  if (words.length !== chars.length) {
    return false;
  }
  const map = new Map();
  const mappedWords = new Set();
  while (words.length > 0) {
    const word = words.pop();
    const char = chars.pop();
    if (map.has(char)) {
      if (map.get(char) !== word) {
        return false;
      }
    } else {
      map.set(char, word);
      if (mappedWords.has(word)) {
        return false;
      }
      mappedWords.add(word);
    }
  }
  return true;
};
```
