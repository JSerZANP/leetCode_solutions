```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findMin = function (nums) {
  // it means to find the first item right?
  // [     m   ][   ] => on the right
  // [   ][ m      ] => on the left

  let i = 0;
  let j = nums.length - 1;
  while (i < j) {
    console.log(i, j);
    const m = Math.floor((i + j) / 2);
    // m -> close to i
    // itself might be the smallet number
    if (nums[m] > nums[j]) {
      i = m + 1;
    } else {
      j = m;
    }
  }
  // [ ]
  // stops when i == j
  return nums[i];
};
```
