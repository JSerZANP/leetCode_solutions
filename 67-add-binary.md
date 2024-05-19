A video explaining this: https://youtu.be/IWok_vEB3I0

```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function (a, b) {
  let carryover = 0;
  let maxLength = Math.max(a.length, b.length);
  let result = Array(maxLength).fill(0);

  let i = 0;

  while (i < maxLength) {
    const sum =
      (a.length - 1 - i < 0 ? 0 : a[a.length - 1 - i] * 1) +
      (b.length - 1 - i < 0 ? 0 : b[b.length - 1 - i] * 1) +
      carryover;
    result[maxLength - 1 - i] = sum % 2;
    carryover = Math.floor(sum / 2);

    i += 1;
  }

  if (carryover > 0) {
    result.unshift(1);
  }

  return result.join("");
};
```

Another try in 2024

```js
/**
 * @param {string} a
 * @param {string} b
 * @return {string}
 */
var addBinary = function (a, b) {
  let carry = 0;
  let lenA = a.length;
  let lenB = b.length;
  let maxLen = Math.max(lenA, lenB);
  let result = "";
  for (let i = 0; i < maxLen; i++) {
    // backward
    let digitA = i < lenA ? a[lenA - 1 - i] : "0";
    let digitB = i < lenB ? b[lenB - 1 - i] : "0";

    let sum = carry + (digitA !== digitB ? 1 : digitA === "1" ? 2 : 0);
    if (sum > 1) {
      carry = 1;
      sum -= 2;
    } else {
      carry = 0;
    }
    result = sum + result;
  }
  if (carry > 0) {
    result = "1" + result;
  }
  return result;
};
```
