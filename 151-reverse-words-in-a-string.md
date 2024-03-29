```js
/**
 * @param {string} s
 * @return {string}
 */
// var reverseWords = function(s) {
//     return s.trim().split(/\s+/).reverse().join(' ')
// };

var reverseWords = function (s) {
  return s.trim().split(/\s+/).reverse().join(" ");
};
```

```js
/**
 * @param {string} s
 * @return {string}
 */
// var reverseWords = function(s) {
//     return s.trim().split(/\s+/).reverse().join(' ')
// };

var reverseWords = function (s) {
  const words = [];
  let isWord = false;
  let buffer = "";

  for (let i = 0; i < s.length; i++) {
    const char = s[i];
    if (isWord) {
      if (char != " ") {
        buffer += char;
      } else {
        isWord = false;
        words.push(buffer);
        buffer = "";
      }
    } else {
      if (char != " ") {
        isWord = true;
        buffer += char;
      }
    }
  }
  if (buffer !== "") {
    words.push(buffer);
  }

  return words.reverse().join(" ");
};
```
