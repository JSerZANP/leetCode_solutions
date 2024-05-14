```js
/**
 * @param {string} ransomNote
 * @param {string} magazine
 * @return {boolean}
 */
var canConstruct = function (ransomNote, magazine) {
  const countMagazine = count(magazine);
  for (const char of ransomNote) {
    const count = (countMagazine.get(char) ?? 0) - 1;
    if (count < 0) {
      return false;
    }
    countMagazine.set(char, count);
  }
  return true;
};

function count(str) {
  const map = new Map();
  for (const char of str) {
    map.set(char, (map.get(char) ?? 0) + 1);
  }
  return map;
}
```
