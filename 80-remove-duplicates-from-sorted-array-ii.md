My explanation on youtube: https://youtu.be/-Td6YPyPqzk

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function (nums) {
  let p1 = 0;
  let p2 = 0;
  let count = 0;

  while (p2 < nums.length) {
    if (nums[p2] !== nums[p2 - 1]) {
      count = 1;
      nums[p1] = nums[p2];
      p1 += 1;
    } else {
      count += 1;
      if (count <= 2) {
        nums[p1] = nums[p2];
        p1 += 1;
      }
    }

    p2 += 1;
  }

  return p1;
};
```
