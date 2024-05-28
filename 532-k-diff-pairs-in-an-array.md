```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findPairs = function (nums, k) {
  // brute force - O(N ^ 2)

  // what if we sort it first?

  // [1, 1, 3, 4, 5] 2

  // 1 1 X
  // 1 3 v
  // now we have to move the window
  // move them to next that is not the same number
  // [3, 4] x
  // [3, 5] v

  // when a range [i, j] < 2
  // then we need to move j to the right
  // if [i, j] > 2, then we need to move [i to the right]

  // O(nlogn), O(n)
  nums.sort((a, b) => a - b);
  let count = 0;
  let i = 0;
  let j = 1;
  const hashes = new Set();
  while (i <= j && j < nums.length) {
    if (i === j) {
      j += 1;
      continue;
    }
    if (nums[j] - nums[i] === k) {
      const hash = `${nums[i]}_${nums[j]}`;
      if (!hashes.has(hash)) {
        count += 1;
        hashes.add(hash);
      }
      i += 1;
      j += 1;
    } else if (nums[j] - nums[i] < k) {
      j += 1;
    } else {
      i += 1;
    }
  }
  return count;
};
```

Or just hashmap.

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */
var findPairs = function (nums, k) {
  const hashes = new Set();
  const numSet = new Set();
  let count = 0;

  // de-dupe by hashes
  // if there are multiple same values
  // only the first two is added
  for (const num of nums) {
    if (numSet.has(num + k)) {
      const hash = `${num}_${num + k}`;
      if (!hashes.has(hash)) {
        count += 1;
        hashes.add(hash);
      }
    }
    if (numSet.has(num - k)) {
      const hash = `${num - k}_${num}`;
      if (!hashes.has(hash)) {
        count += 1;
        hashes.add(hash);
      }
    }
    numSet.add(num);
  }
  return count;
};
```
