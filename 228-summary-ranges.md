Youtube video explaining this: https://youtu.be/H1zJFRITZgA

```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function (nums) {
  const result = [];

  for (let i = 0; i < nums.length; i++) {
    let end = i;
    while (nums[end + 1] === nums[end] + 1) {
      end += 1;
    }

    if (end > i) {
      result.push(`${nums[i]}->${nums[end]}`);
    } else {
      result.push(`${nums[i]}`);
    }

    i = end;
  }

  return result;
};
```

Another try

```js
/**
 * @param {number[]} nums
 * @return {string[]}
 */
var summaryRanges = function (nums) {
  if (nums.length === 0) return [];

  const intervals = [];
  let buffer = [nums[0], nums[0]];
  for (let i = 1; i < nums.length; i++) {
    const num = nums[i];
    if (num === buffer[1] + 1) {
      buffer[1] = num;
    } else {
      intervals.push(buffer);
      buffer = [num, num];
    }
  }
  intervals.push(buffer);

  return intervals.map(([start, end]) =>
    start === end ? `${start}` : `${start}->${end}`
  );
};
```
