### 1. brute force

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {void} Do not return anything, modify nums in-place instead.
 */
// O(k * N)
var rotate = function (nums, k) {
  while (k > 0) {
    nums.unshift(nums.pop());
    k -= 1;
  }
};
```

### 2. reverse

```js
// [1,2,3,4,5,6,7]
// [1,2 3,1,5,6,7] 4 at 3
// [1,2,3,1,5,3,4] 6 at 5
// [1,6,3,1,5,3,4] 2 at 1

// so we can update the item and try put the next item at right location

// we can keep swaping the nums and update the indices as well.
var rotate = function (nums, k) {
  k %= nums.length;
  if (k === 0) return;
  reverse(0, nums.length - 1);
  reverse(0, k - 1);
  reverse(k, nums.length - 1);

  function reverse(i, j) {
    while (i < j) {
      [nums[i], nums[j]] = [nums[j], nums[i]];
      i += 1;
      j -= 1;
    }
  }
};
```
