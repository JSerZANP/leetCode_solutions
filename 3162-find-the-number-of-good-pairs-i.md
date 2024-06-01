```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @param {number} k
 * @return {number}
 */

// O(mn)
var numberOfPairs = function (nums1, nums2, k) {
  let result = 0;
  nums1.forEach((a) => {
    nums2.forEach((b) => {
      if (b * k !== 0 && a % (b * k) === 0) {
        result += 1;
      }
    });
  });
  return result;
};
```
