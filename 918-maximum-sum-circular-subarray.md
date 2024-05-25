```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubarraySumCircular = function (nums) {
  // if the target subarray lies in the base range
  // we can just get the result in one pass

  // if somehow we go beyond the last element
  // it means the larges sum of two lists
  // 1. starting from backward, the last item
  // 2. starting from first item.
  // There must be no overlap.

  // so we need two arrays
  // maxSumUntil and maxSumSince
  // these could be derived in one pass

  let i = 0;
  let j = 0;
  let sum = 0;
  let max = -Infinity;

  while (j < nums.length && i < nums.length) {
    sum += nums[j];
    max = Math.max(max, sum);
    if (sum < 0) {
      sum = 0;
      i = j + 1;
      j = j + 1;
    } else {
      j = j + 1;
    }
  }

  const maxWithinRange = max;

  j = 0;
  sum = 0;
  max = -Infinity;
  const maxSumUntil = [];
  while (j < nums.length) {
    sum += nums[j];
    max = Math.max(max, sum);
    // we cannot break here
    // if (sum < 0) {
    //     break
    // }
    maxSumUntil[j] = max;
    j += 1;
  }

  j = 0;
  sum = 0;
  max = -Infinity;
  const maxSumSince = [];
  while (j < nums.length) {
    sum += nums[nums.length - 1 - j];
    max = Math.max(max, sum);
    // we cannot break here
    // if (sum < 0) {
    //     break
    // }
    maxSumSince[j] = max;
    j += 1;
  }

  // now get the maximum

  let maxWithReturn = -Infinity;
  for (let i = 0; i < maxSumSince.length; i++) {
    const maxSumUntilIndex = nums.length - 1 - i - 1;
    if (maxSumUntilIndex < 0 || maxSumUntil.length === 0) {
      // no items for the left
      break;
    }
    const max =
      maxSumUntilIndex < maxSumUntil.length
        ? maxSumUntil[maxSumUntilIndex]
        : maxSumUntil.at(-1);
    const sum = maxSumSince[i] + max;
    maxWithReturn = Math.max(maxWithReturn, sum);
  }

  return Math.max(maxWithReturn, maxWithinRange);
};
```
