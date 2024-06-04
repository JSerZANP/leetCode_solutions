```js
/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
var isOneEditDistance = function (s, t) {
  // suppose the result is true
  // then there are 3 patterns

  // [  A ][  B ]
  // [  A ] [ B  ]

  // [  A]C[   B]
  // [  A][   B]

  // [  A]D[   B]
  // [  A]E[   B]

  // we can compare the prefix and postfix
  let i = 0;
  while (i < s.length && i < t.length) {
    if (s[i] === t[i]) {
      i += 1;
    } else {
      break;
    }
  }
  // when it stops, either one is done, or first different character
  if (i === s.length) return t.length - s.length === 1;
  if (i === t.length) return s.length - t.length === 1;

  let j = 0;
  while (i < s.length && j < t.length) {
    if (s[s.length - 1 - j] === t[t.length - 1 - j]) {
      j += 1;
    } else {
      break;
    }
  }
  // when it stops, either one is done, or first different character
  if (j === s.length) return t.length - s.length === 1;
  if (j === t.length) return s.length - t.length === 1;

  // now we check the patterns.

  // [  A]D[   B]
  // [  A]E[   B]
  if (s.length === t.length && i + j === s.length - 1) {
    return true;
  }

  // [  A ][  B ]
  // [  A ] [ B  ]
  const shorter = s.length < t.length ? s : t;
  const longer = s.length > t.length ? s : t;
  if (i + j === shorter.length && longer.length === shorter.length + 1) {
    return true;
  }
  return false;
};
```
