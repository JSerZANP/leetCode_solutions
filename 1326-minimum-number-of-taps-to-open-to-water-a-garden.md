```js
/**
 * @param {number} n
 * @param {number[]} ranges
 * @return {number}
 */
var minTaps = function (n, ranges) {
  // let's think how we can cover one single garden
  // we need to get the ranges that covers it.
  // if we sort the ranges first, as showned in the example
  // we'll see that we have to choose the one of the longest ranges to cover garden 0
  // then obviously we need to choose the one with largest right boundary which already covers garden 5

  // suppose the range only covers up to 3, then we need to find next range that covers 4

  // now it is clear
  // sort the ranges
  // for each garden from left to right
  // search the ranges that covers each garden, choose the one that has larges right boundary
  // skip the already covered gardens

  const intervals = ranges
    .map((range, i) => [i - range, i + range])
    .sort((a, b) => a[0] - b[0]);

  let nextGardenToCover = 0;
  let result = 0;
  let intervalIndex = 0;

  while (nextGardenToCover < n) {
    // console.log(intervalIndex, nextGardenToCover, intervals)
    let covered = false;
    let newNextGardenToCover = nextGardenToCover;
    while (
      intervalIndex < intervals.length &&
      intervals[intervalIndex][0] <= nextGardenToCover
    ) {
      // console.log(intervals[intervalIndex])
      if (intervals[intervalIndex][1] >= nextGardenToCover) {
        covered = true;
      }
      newNextGardenToCover = Math.max(
        newNextGardenToCover,
        intervals[intervalIndex][1]
      );
      intervalIndex += 1;
    }
    // console.log('covered', covered, nextGardenToCover)
    if (!covered) {
      return -1;
    }
    result += 1;
    nextGardenToCover = newNextGardenToCover;
  }

  return result;
};
```
