Me explaining this: https://youtu.be/bC4H5GYwUYI

```js
/**
 * @param {number[]} target
 * @param {number[]} arr
 * @return {boolean}
 */

// Time: O(m + n)
// Space: worst O(m + n)
// var canBeEqual = function(target, arr) {
//     // count
//     const count1 = new Map()
//     const count2 = new Map()

//     for (let i of target) {
//       if (count1.has(i)) {
//         count1.set(i, count1.get(i) + 1)
//       } else {
//         count1.set(i, 1)
//       }
//     }

//     for (let i of arr) {
//       if (count2.has(i)) {
//         count2.set(i, count2.get(i) + 1)
//       } else {
//         count2.set(i, 1)
//       }
//     }

//     for (let [i, count] of count1) {
//       if (count2.get(i) !== count) {
//         return false
//       }
//     }

//     return true
// };

// sort
// Time: O(2mlogm + m) => O(mlom)
// Space: O(1)
var canBeEqual = function (target, arr) {
  if (target.length !== arr.length) return false;
  // count
  target.sort((a, b) => a - b);
  arr.sort((a, b) => a - b);

  for (let i = 0; i < target.length; i++) {
    if (arr[i] !== target[i]) {
      return false;
    }
  }

  return true;
};
```
