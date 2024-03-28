## 1.

Video explaining this: https://youtu.be/dNDqJ-vtB18

```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function (nums1, m, nums2, n) {
  const totalLen = m + n;

  let i = 0;
  let j = 0;

  while (j < nums2.length) {
    const index1 = m - 1 - i;
    const index2 = n - 1 - j;
    const index = m + n - 1 - (i + j);

    if (index1 > -1 && nums1[index1] >= nums2[index2]) {
      nums1[index] = nums1[index1];
      i += 1;
    } else {
      nums1[index] = nums2[index2];
      j += 1;
    }
  }

  return nums1;
};
```

## 2. Three pointers - easy to understand

```js
var merge = function (nums1, m, nums2, n) {
  // [1,2,3,0,0,0], [2,5,6]
  // [1,2, 2, 3, 5, 6]

  // [0, 0, 0, 1, 2, 3], [2, 5, 6]
  // [1, 2, 2, 3, 5, 6]

  // [1,2,3,0,0,0] , [2, 5, 6]
  // [ 12, 2 3, 5,6]

  let p1 = m - 1;
  let p2 = n - 1;
  let p = m + n - 1;

  while (p1 >= 0 || p2 >= 0) {
    if (p1 >= 0 && p2 >= 0) {
      if (nums1[p1] >= nums2[p2]) {
        nums1[p] = nums1[p1];
        p1 -= 1;
      } else {
        nums1[p] = nums2[p2];
        p2 -= 1;
      }
    } else if (p1 >= 0) {
      nums1[p] = nums1[p1];
      p1 -= 1;
    } else {
      nums1[p] = nums2[p2];
      p2 -= 1;
    }

    p -= 1;
  }
};
```
