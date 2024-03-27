```js
var topKFrequent = function (nums, k) {
  const map = new Map();
  for (const num of nums) {
    map.set(num, (map.get(num) || 0) + 1);
  }

  nums = [...map.keys()];
  // quick sort on nums array
  // but drop the half in which k doesn't fall into

  let i = 0;
  let j = nums.length - 1;
  // console.log(nums)
  while (i <= j) {
    // console.log(i, j)
    const pivotIndex = i + Math.floor(Math.random() * (j + 1 - i));
    const pivotNum = nums[pivotIndex];
    // arrange numbers so that numbers
    // numbers to the left of pivot have larger occurance than pivot
    // while numbers to the right of pivot have smaller occurance
    // to do this, we keep swaping

    let start = i;
    let end = j;

    while (start <= end) {
      // console.log('start', start, 'end', end, 'pivot', pivotNum)
      if (map.get(nums[start]) >= map.get(pivotNum)) {
        start += 1;
      } else {
        [nums[start], nums[end]] = [nums[end], nums[start]];
        end -= 1;
      }
    }
    // when above stops,
    // nums at end + 1 and after are smaller than pivot
    // end is the last number larger than pivot
    // what if the numbers are all the same?
    //
    // console.log('now end', end)
    if (end + 1 === k) {
      return nums.slice(0, end + 1);
    } else if (end + 1 > k) {
      // too many candidates
      j = end;
    } else {
      // too few candiates, then select on the lower end
      i = end + 1;
    }
  }

  // when above stops and not yet returned
  // it should not be?
};
```
