## 1.

A video explaining this: https://youtu.be/ZuvCatYDRyk

```js
/**
 * @param {string} s
 * @return {number}
 */

// state machine
// Time: O(n)
// Space: O(1)
var lengthOfLastWord = function (s) {
  // 'whiteSpace'
  // 'word'

  let state = "whiteSpace";
  let startIndexOfWord = -1;
  let lastLength = 0;

  for (let i = 0; i < s.length + 1; i++) {
    // end of word
    if ((s[i] === " " || i === s.length) && state !== "whiteSpace") {
      if (startIndexOfWord > -1) {
        lastLength = i - startIndexOfWord;
      }
      state = "whiteSpace";
    }

    // start of word
    if (s[i] !== " " && state !== "word") {
      startIndexOfWord = i;
      state = "word";
    }
  }

  return lastLength;
};
```

## 2

```js
// /**
//  * @param {string} s
//  * @return {number}
//  */
// var lengthOfLastWord = function(s) {
//     const trimed = s.trim()
//     if (trimed.length == 0) return ''

//     return trimed.split(' ').slice(-1)[0].length
// };

/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLastWord = function (s) {
  let endIndex = null;
  for (let i = s.length - 1; i >= -1; i--) {
    const char = s[i];
    if (endIndex != null) {
      if (char === " " || i === -1) {
        return endIndex - (i + 1) + 1;
      }
    } else {
      if (char !== " ") {
        endIndex = i;
      }
    }
  }
};
```
