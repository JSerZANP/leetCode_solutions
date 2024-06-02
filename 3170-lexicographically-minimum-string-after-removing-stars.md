```js
/**
 * @param {string} s
 * @return {string}
 */
var clearStars = function (s) {
  // aaba**zz*
  // remove the smallest, if multiple, choose the right most one
  // array 26 to hold the right most index?

  // a [0]
  // b [2]
  // z [2]

  // deleted Set to hold the index

  const indicesArr = [];
  const deletedIndices = new Set();
  const charCodeA = "a".charCodeAt(0);

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (char === "*") {
      for (let i = 0; i < 26; i++) {
        if (indicesArr[i]?.length > 0) {
          deletedIndices.add(indicesArr[i].pop());
          break;
        }
      }
    } else {
      const j = s.charCodeAt(i) - charCodeA;
      if (indicesArr[j] == null) {
        indicesArr[j] = [];
      }
      indicesArr[j].push(i);
    }
  }
  let result = "";
  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (char !== "*" && !deletedIndices.has(i)) {
      result += char;
    }
  }
  return result;
};
```
