Me explaining it on youtube: https://youtu.be/6GgZbjcBCEk

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @param {number} x
 * @return {number[]}
 */

// Time: O(log N) + k^2
var findClosestElements = function (arr, k, x) {
  // find the position o x, and expand in two directions

  // [, 3] => 3
  // [-Infinity, 1] => -1

  // binary search
  arr.unshift(-Infinity);
  arr.push(Infinity);

  let i = 0;
  let j = arr.length;

  while (j - i > 1) {
    const middle = Math.floor((i + j) / 2);
    if (arr[middle] === x) {
      i = middle - 1;
      j = middle;
      break;
    } else if (arr[middle] < x) {
      i = middle;
    } else {
      j = middle;
    }
  }

  // now get [i, j] which x is at j, or right before j
  let count = 0;
  while (count < k) {
    if (Math.abs(arr[i] - x) <= Math.abs(arr[j] - x)) {
      i -= 1;
    } else {
      j += 1;
    }
    count += 1;
  }

  return arr.slice(i + 1, j);
};
```

Another try in 2024

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @param {number} x
 * @return {number[]}
 */
// [1,2,3,4,5], k = 4, x = 3
var findClosestElements = function (arr, k, x) {
  // x might exist or not
  // find the index or insert position
  // expand in two directions, two cursor
  const pos = getPos(arr, x); // 1
  let i = pos - 1; // might be negative // 1
  let j = pos; // 4
  let result = []; //

  while (result.length < k) {
    const left = arr[i] ?? Infinity;
    const right = arr[j] ?? Infinity;
    if (Math.abs(left - x) <= Math.abs(right - x)) {
      result.unshift(arr[i]);
      i -= 1;
    } else {
      result.push(arr[j]);
      j += 1;
    }
  }
  return result;
};

function getPos(arr, x) {
  // [1,2,3,4,5], 3
  let i = 0; // 0
  let j = arr.length - 1; // 4
  while (i <= j) {
    const m = Math.floor((i + j) / 2); // 2
    if (arr[m] === x) {
      return m; // 2
    }
    if (x > arr[m]) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }
  // when it stops , item at j smaller than x, ietm at i > x
  return i;
}
```
