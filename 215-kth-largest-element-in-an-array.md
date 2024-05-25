me explaining this on youtube: https://youtu.be/mvPR0p0WGe8

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */

// Time: O(n log n)
// var findKthLargest = function(nums, k) {
//     // sort first
//     nums.sort((a, b) => b - a)
//     return nums[k - 1]
// };

// 3, 2, 1, 5, 6, 4
// 3, 5, 6, 4, 2, 1
// 4, 5, 6, 3, 2, 1
// 5, 6, 4, 3, 2, 1
// 6, 5, 4, 3, 2, 1

// fast short-circuit with quick sort
// Time: O(n ^ 2), average: n ( 1 + 1/2 + 1/4) =
// 1 + 1 / 2 + 1 /2 ^ 2 + ..+ 1 / 2 ^ n = s
// 1/2 + 1/2 ^ 2 ... 1/2 ^ n + 1/2^n +1 = s/2
// 1 - 1/2^(n + 1) = s/2
// s = 2 - 1/2^n
// ns = 2n - n/2^n
// ~O(n)
// Space: O(1)
var findKthLargest = function (nums, k) {
  // use quick sort
  // if pivot happen to be the k-th, just return
  // if not, search half of them

  let start = 0;
  let end = nums.length - 1;

  const swap = (i, j) => {
    [nums[i], nums[j]] = [nums[j], nums[i]];
  };

  // [1, 5, 4, 2]
  //
  while (start <= end) {
    const pivot = nums[start];
    let indexToSwap = start + 1;

    for (let i = start + 1; i <= end; i++) {
      if (nums[i] >= pivot) {
        swap(indexToSwap, i);
        indexToSwap += 1;
      }
    }

    swap(start, indexToSwap - 1);

    if (indexToSwap - 1 === k - 1) {
      return pivot;
    }

    if (indexToSwap - 1 < k - 1) {
      start = indexToSwap;
    } else {
      end = indexToSwap - 2;
    }
  }
};
```

Another try in 2024. TLE

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findKthLargest = function (nums, k) {
  // quick select
  // similar to quick sort
  // we choose a pivot and put smaller ones on left, larger ones on right
  // if this pivot happen to be the right position
  // then it is
  return findKthLargestImpl(nums, 0, nums.length - 1, k);
};

// k is 1-based
function findKthLargestImpl(nums, start, end, k) {
  // console.log('findKthLargestImpl', nums, start, end, nums.slice(start, end + 1), k)
  // search the kth item from range [i, j]

  // one round of pivoting
  let pivot = nums[start];
  let indexToSwap = start + 1;

  for (let j = start + 1; j <= end; j++) {
    if (nums[j] >= pivot) {
      [nums[indexToSwap], nums[j]] = [nums[j], nums[indexToSwap]];
      indexToSwap += 1;
    }
    // console.log(j, nums)
  }
  [nums[indexToSwap - 1], nums[start]] = [nums[start], nums[indexToSwap - 1]];
  // now elements on the left are all bigger or equal to the pivot
  // wait actually indexToSwap - 1 is our search?
  // console.log(nums, indexToSwap)
  if (indexToSwap - 1 === k - 1) {
    return nums[indexToSwap - 1];
  } else if (indexToSwap - 1 < k - 1) {
    return findKthLargestImpl(nums, indexToSwap, end, k);
  } else {
    return findKthLargestImpl(nums, start, indexToSwap - 2, k);
  }
}
```
