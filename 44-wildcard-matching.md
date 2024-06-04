Youtube video explaining this: https://youtu.be/wM_PMOwlufc

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function (s, p) {
  const match = (i, j) => {
    if (i >= s.length && j >= p.length) {
      return 0;
    }
    // adasdasd aa  dsadasd aa dd ba  dd a asdfas  bbaa
    // *        aa    *      ba  *  a     *   bb
    if (i < s.length && (s[i] === p[j] || p[j] === "?")) {
      return match(i + 1, j + 1);
    } else if (p[j] === "*") {
      // skip the sequential *
      while (p[j + 1] === "*") {
        j += 1;
      }

      for (let k = i; k <= s.length; k++) {
        const result = match(k, j + 1);
        if (result === 0) {
          return 0;
        } else if (result === 1) {
          break;
        }
      }

      return 1;
    }

    return -1;
  };

  return match(0, 0) === 0;
};
```

Another try in 2024

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function (s, p) {
  // keep two cursors for two strings
  // move forward if matches
  // fail if not match
  // ? : match every letter
  // * : recursively match all the positions
  const cache = new Array(s.length + 1)
    .fill(0)
    .map((_) => new Array(p.length + 1).fill(null));

  function matchFromImpl(i, j) {
    if (i === s.length && j === p.length) {
      return true;
    }
    if (i === s.length) {
      if (p[j] === "*") {
        return matchFrom(i, j + 1);
      }
      return j === p.length;
    }

    if (p[j] === "?") {
      return matchFrom(i + 1, j + 1);
    }
    if (p[j] === "*") {
      // skip consecutive '*'
      while (p[j + 1] === "*") {
        j += 1;
      }
      for (let k = i; k <= s.length; k++) {
        if (matchFrom(k, j + 1)) {
          return true;
        }
      }
      return false;
    }
    if (s[i] === p[j]) {
      return matchFrom(i + 1, j + 1);
    }
    return false;
  }

  function matchFrom(i, j) {
    if (cache[i][j] != null) {
      return cache[i][j];
    }
    const result = matchFromImpl(i, j);
    cache[i][j] = result;
    return result;
  }
  return matchFrom(0, 0);
};
```
