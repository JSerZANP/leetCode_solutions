Here is a video explaining this: https://youtu.be/GBaPjaZ12Qk

```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function (nums) {
  // counting + rewrite
  // 2O(n)
  // O(1)

  // sort method
  // O(nlogn)

  //  2 0 2 1 1 0
  //

  // Time: O(n)
  // Space: O(1)

  let i = 0; // left most index
  let j = nums.length - 1; // right most index
  let k = 0; // index to loop

  while (k <= j) {
    switch (nums[k]) {
      case 0: // swap it with left most index
        if (k > i) {
          [nums[k], nums[i]] = [nums[i], nums[k]];
        } else {
          k += 1;
        }
        i += 1;
        break;
      case 2: // swap it with right most index
        if (k < j) {
          [nums[k], nums[j]] = [nums[j], nums[k]];
        } else {
          k += 1;
        }
        j -= 1;
        break;
      case 1:
        k += 1;
        break;
    }
  }
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function (nums) {
  // 2,0,2,1,1,0
  // 0, 0 2 1 1 2
  // 0, 0 1 1 2 2

  // swap with head if 0
  // swap with tail if 2

  function swap(i, j) {
    [nums[i], nums[j]] = [nums[j], nums[i]];
  }
  let p1 = 0;
  let p2 = nums.length - 1;
  let p = 0;
  while (p <= p2) {
    if (nums[p] === 2) {
      swap(p2, p);
      p2 -= 1;
    } else {
      p += 1;
    }
  }
  while (p >= p1) {
    if (nums[p] === 0) {
      swap(p1, p);
      p1 += 1;
    } else {
      p -= 1;
    }
  }
};
```
