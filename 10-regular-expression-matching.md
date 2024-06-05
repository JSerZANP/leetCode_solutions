A video explaining this: https://youtu.be/yTB92FXcopc

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {boolean}
 */
var isMatch = function (s, p) {
  const check = (s, p, i, j) => {
    // aaa vs a*a*a*a*
    if (j > p.length - 1) {
      return i > s.length - 1;
    }

    const isNextQuantiyModifier = p[j + 1] === "*";

    if (!isNextQuantiyModifier) {
      if ([s[i], "."].includes(p[j])) {
        return i < s.length && check(s, p, i + 1, j + 1);
      } else {
        return false;
      }
    } else {
      // aa vs a*, finally 2 vs 0
      if ([s[i], "."].includes(p[j])) {
        return check(s, p, i, j + 2) || (i < s.length && check(s, p, i + 1, j));
      } else {
        return check(s, p, i, j + 2);
      }
    }
  };

  return check(s, p, 0, 0);
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
  // aa a => a "" => no
  // aa a* => a * => * zero or more of a => ok

  function matchFromImpl(i, j) {
    // p needs to finish first, a vs ab*
    if (j === p.length) {
      return i === s.length;
    }

    // when we compare a character, we need to consider the quantifier
    if (p[j + 1] === "*") {
      if (p[j] === "." || p[j] === s[i]) {
        // we don't need to check every other indices, because it is already included in the next calls
        // also be careful about the `i < s.length`, because we stay at j, we cannot move beyond s
        // that will be covered in the first matchFrom(i, j + 2)
        return matchFrom(i, j + 2) || (i < s.length && matchFrom(i + 1, j));
      } else {
        return matchFrom(i, j + 2);
      }
    } else {
      // no quantifier
      if (p[j] === s[i] || p[j] === ".") {
        return matchFrom(i + 1, j + 1);
      }
    }
    return false;
  }

  const cache = new Map();
  function matchFrom(i, j) {
    const key = `${i}_${j}`;
    if (cache.has(key)) {
      return cache.get(key);
    } else {
      const result = matchFromImpl(i, j);
      cache.set(key, result);
      return result;
    }
  }
  return matchFrom(0, 0);
};
```
