My video explaining this: https://youtu.be/bk1NdxowB6M

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// DP
// Time: O(n)
// Space: O(n)
var maxSubArray = function (nums) {
  // f(n) means maximum subarray ending at index n

  // f(n) === Math.max(f(n - 1) + nums[n], nums[n])

  // maximun = Math.max(f(n))

  let maxes = Array(nums.length).fill(Number.NEGATIVE_INFINITY);
  maxes[0] = nums[0];
  let maximum = nums[0];

  for (let i = 1; i < nums.length; i++) {
    if (maxes[i - 1] <= 0) {
      maxes[i] = nums[i];
    } else {
      maxes[i] = maxes[i - 1] + nums[i];
    }

    maximum = Math.max(maximum, maxes[i]);
  }

  return maximum;
};
```

```js
// Divide and conquer

var maxSubArray = function (nums) {
  const max = (i, j) => {
    if (i === j) return nums[i];

    const middle = Math.floor((i + j) / 2);

    let maxLeft = nums[middle];
    let sumLeft = nums[middle];
    for (let k = middle - 1; k > -1; k--) {
      sumLeft += nums[k];
      maxLeft = Math.max(sumLeft, maxLeft);
    }

    let maxRight = nums[middle + 1];
    let sumRight = nums[middle + 1];
    for (let k = middle + 2; k < nums.length; k++) {
      sumRight += nums[k];
      maxRight = Math.max(sumRight, maxRight);
    }

    return Math.max(maxLeft + maxRight, max(i, middle), max(middle + 1, j));
  };

  return max(0, nums.length - 1);
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
  // [-2,1,-3,4,-1,2,1,-5,4]
  // [-2], < 0, we don't start from 1
  //    [1] ok
  //    [1, -3] => sum is negative no
  //          [4, -1, 2, 1] candidate

  // lets focus on where it starts

  //        [i....j]
  // there must not be some consecutive numbers that sum is negative before it
  // meaning if [i...j] sum is negative, it cannot start from i
  // how about i + 1?
  // nope because [i, i+1], [i, i+ 2]...[i, ...j-1] are all checked before it
  // so we can skip all the numbers go to k + 1

  // i, j
  // accumulate the sum

  let i = 0;
  let j = 0;
  let sum = 0;
  // it should not be empty
  let max = -Infinity;
  while (j < nums.length) {
    sum += nums[j];
    max = Math.max(sum, max);
    if (sum > 0) {
      j += 1;
    } else {
      sum = 0;
      i = j + 1;
      j += 1;
    }
  }
  return max;
};
``;
```
