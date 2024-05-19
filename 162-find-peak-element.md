Here is my youtube video explaining this: https://youtu.be/RnxuoWbs_v8

```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(logn)
// spaceL O(1)
var findPeakElement = function (nums) {
  // binary search

  //  1 2 3 4

  let start = 0;
  let end = nums.length - 1;

  while (start <= end) {
    const middle = Math.floor((start + end) / 2);
    if (nums[middle] < nums[middle + 1]) {
      start = middle + 1;
    } else {
      end = middle - 1;
    }
  }

  // ends when start > end
  return start;
};
```

Another try

```js
/**
 * @param {number[]} nums
 * @return {number}
 */
var findPeakElement = function (nums) {
  // fine 1 peak element is enough

  // since two numbers at both side are -Infinity
  // if there is one number => then it's the target
  // if two numbers => bigger one is the target
  // if three numbers =>

  // [a, b, c] =>

  // it means every sequence has a peak element
  // because when we add the first element, it adds a peak
  // later each number being added are just adding new peaks
  // or while disabling an existing peak

  // also if a number smaller than next one,
  // we can think about theumber as -Infinity
  // there is a peak after it

  // if a number  smaller than previous one

  // there is a peak before it

  // if a numbeer smaller than both, then either side is fun

  // Binary search
  let i = 0;
  let j = nums.length - 1;

  while (i <= j) {
    const mid = Math.floor((i + j) / 2);
    if (
      nums[mid] > (nums[mid - 1] ?? -Infinity) &&
      nums[mid] > (nums[mid + 1] ?? -Infinity)
    ) {
      return mid;
    }
    if (nums[mid] < (nums[mid - 1] ?? -Infinity)) {
      j = mid - 1;
    } else {
      i = mid + 1;
    }
  }

  // when i j meets, it must be the peak
  return i;
};
```
