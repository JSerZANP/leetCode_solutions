A video explaining this: https://youtu.be/_Df1OgaqPPg

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var pivotIndex = function (nums) {
  if (nums.length === 0) return -1;
  if (nums.length === 1) return 1;

  // get the sum array from left to right
  let sumAll = 0;
  for (let i = 0; i < nums.length; i++) {
    sumAll += nums[i];
  }

  let sumLeft = 0;
  for (let k = 0; k < nums.length; k++) {
    if (k > 0) {
      sumLeft += nums[k - 1];
    }

    if (sumLeft * 2 + nums[k] === sumAll) {
      return k;
    }
  }
  return -1;
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var pivotIndex = function (nums) {
  // we need to know the sum until and sum since
  // since we need to return the leftmost
  // we can first check sum since

  // inclusive.
  let sumSince = new Array(nums.length + 1).fill(0);
  let sum = 0;
  for (let i = nums.length - 1; i >= 0; i--) {
    sum += nums[i];
    sumSince[i] = sum;
  }
  sum = 0;
  for (let i = 0; i < nums.length; i++) {
    if (sum === sumSince[i + 1]) {
      return i;
    }
    sum += nums[i];
  }
  return -1;
};
```
