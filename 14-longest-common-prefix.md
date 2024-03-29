## 1

A video explaining this: https://youtu.be/enprkdKA7uU

```js
/**
 * @param {string[]} strs
 * @return {string}
 */
var longestCommonPrefix = function (strs) {
  if (strs.length === 0) {
    return "";
  }

  let isShortestStrMet = false;
  let i = 0;
  for (; i < strs[0].length; i++) {
    if (isShortestStrMet) {
      break;
    }

    const char = strs[0][i];
    let isSame = true;
    for (let j = 0; j < strs.length; j++) {
      isShortestStrMet = strs[j][i] === undefined;

      if (strs[j][i] !== char) {
        isSame = false;
        break;
      }
    }

    if (!isSame) {
      break;
    }
  }

  return strs[0].slice(0, i);
};
```

## 2

```js
var longestCommonPrefix = function (strs) {
  let result = "";

  let i = 0;
  while (true) {
    let char;
    for (const str of strs) {
      if (i >= str.length) {
        return result;
      }
      if (char == null) {
        char = str[i];
      } else if (char !== str[i]) {
        return result;
      }
    }
    result += char;
    i += 1;
  }
};
```
