A detailed explanation in this video https://youtu.be/jzcD-LbTXJA

```js
/**
 * @param {string} haystack
 * @param {string} needle
 * @return {number}
 */
// O(nm)
// var strStr = function(haystack, needle) {
//     if (needle === '') return 0

//     // O(n)
//     for (let i = 0; i < haystack.length; i++) {
//       let j = 0;
//       // O(m)
//       while (j < needle.length && needle[j] === haystack[i + j]) {
//         j += 1
//       }
//       if (j === needle.length) {
//         return i
//       }
//     }

//     return -1
// };

// O(n + m)   ==> KMP
var strStr = function (haystack, needle) {
  if (needle === "") return 0;

  const jumpStep = [0, 0];

  let l = 1;
  let k = 0;
  // O(m)
  // ababcaabc
  //  ababcaabc
  // jump[i] means if we don't match at i,
  // where should we compare next
  // the generation of jump is just similar to the search
  while (l < needle.length) {
    if (needle[l] === needle[k]) {
      l += 1;
      k += 1;
      jumpStep[l] = k;
    } else if (k === 0) {
      l += 1;
      jumpStep[l] = 0;
    } else {
      k = jumpStep[k];
    }
  }

  let i = 0;
  let j = 0;

  // O(n)
  while (i < haystack.length && j < needle.length) {
    if (haystack[i] === needle[j]) {
      i += 1;
      j += 1;
      if (j === needle.length) {
        return i - needle.length;
      }
    } else if (j > 0) {
      j = jumpStep[j];
    } else {
      i += 1;
    }
  }

  return -1;
};
```
