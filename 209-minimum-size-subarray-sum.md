Here is my youtube explaining this: https://youtu.be/eUdoZnemqFQ

```js
/**
 * @param {number} s
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(2N) => O(N)
// space: O(1)
var minSubArrayLen = function (s, nums) {
  if (nums.length === 0) return 0;
  // 2
  // 2 3
  // 2 3 1
  // 2 3 1 2
  //   3 1 2 4
  //     1 2 4
  //       2 4 3
  //         4 3

  // sliing window

  let currentLen = 0;
  let currentSum = 0;

  let minLen = Infinity;

  let start = 0;
  let end = 0;

  while (end < nums.length) {
    currentLen += 1;
    currentSum += nums[end];
    if (currentSum >= s) {
      do {
        minLen = Math.min(minLen, end - start + 1);
        currentSum -= nums[start];
        start += 1;
      } while (currentSum >= s);
    }
    end += 1;
  }

  return minLen === Infinity ? 0 : minLen;
};
```

Maybe following is easier to understand.

```js
var minSubArrayLen = function (target, nums) {
  // [2,3,1,2,4,3]
  // []

  let i = 0; // 5
  let j = 0; // 6
  let sum = nums[0]; // 7
  let result = Infinity; // 2

  while (i < nums.length && j < nums.length) {
    if (sum >= target) {
      result = Math.min(result, j - i + 1);
      sum -= nums[i];
      i += 1;
    } else {
      j += 1;
      sum += nums[j];
    }
  }
  return Number.isFinite(result) ? result : 0;
};
```
