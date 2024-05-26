```js
/**
 * @param {string} s
 * @param {string} t
 * @return {number}
 */
var minSteps = function (s, t) {
  // count? and differentiate?
  const countS = count(s);
  const countT = count(t);
  let coutOfCharToAdd = 0;
  let coutOfCharToDelete = 0;
  for (let i = 0; i < countS.length; i++) {
    if (countT[i] > countS[i]) {
      coutOfCharToDelete += countT[i] - countS[i];
    }

    if (countT[i] < countS[i]) {
      coutOfCharToAdd += countS[i] - countT[i];
    }
  }

  // we can replace the character from add to remove
  //coutOfCharToDelete must be the same as coutOfCharToAdd
  // because s and t are of same length
  return coutOfCharToAdd;
};

function count(s) {
  const result = new Array(26).fill(0);
  const charCodeA = "a".charCodeAt(0);
  for (let i = 0; i < s.length; i++) {
    const charCode = s.charCodeAt(i);
    result[charCode - charCodeA] += 1;
  }
  return result;
}
```
