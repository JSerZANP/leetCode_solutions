```js
/**
 * @param {string} word
 * @return {string}
 */
var compressedString = function (word) {
  // maintain a buffer
  // flush on new character, or last one, or buffer is overflowed
  let result = "";
  let buffer = "";
  let count = 0;
  for (const char of word) {
    if (buffer === "") {
      buffer = char;
      count += 1;
    } else if (char !== buffer[0]) {
      result += count + buffer;
      buffer = char;
      count = 1;
    } else {
      if (count === 9) {
        result += count + buffer;
        count = 1;
      } else {
        count += 1;
      }
    }
  }
  if (count > 0) {
    result += count + buffer;
  }
  return result;
};
```
