## 1. Put the item at correct position

A video explaining this: https://youtu.be/PTLuyqH2VkM

```js
/**
 * @param {number[]} nums
 * @param {number} val
 * @return {number}
 */
var removeElement = function (nums, val) {
  let p1 = 0;
  let p2 = 0;

  while (p2 < nums.length) {
    if (nums[p2] !== val) {
      nums[p1] = nums[p2];
      p1 += 1;
    }

    p2 += 1;
  }

  return p1;
};
```

## 2. Swap with the last item

```js
var removeElement = function (nums, val) {
  // swap the val with last element
  let i = 0;
  let j = nums.length - 1;
  while (i <= j) {
    if (nums[i] === val) {
      swap(i, j);
      j -= 1;
    } else {
      i += 1;
    }
  }

  // j is to be non val
  // i is to be the val

  function swap(i, j) {
    [nums[i], nums[j]] = [nums[j], nums[i]];
  }

  return j + 1;
};
```
