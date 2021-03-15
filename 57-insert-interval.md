Here is a video explaining this: https://youtu.be/FyFdPQ_v31s

```js
/**
 * @param {number[][]} intervals
 * @param {number[]} newInterval
 * @return {number[][]}
 */
var insert = function(intervals, newInterval) {
    // only need to find the position
    // insert
    // check and merge as 56
    
    let targetIndex = 0
    let start = 0
    let end = intervals.length - 1
    while (start <= end) {
      const middle = Math.floor((start + end) / 2)
      if (intervals[middle][0] >= newInterval[0]) {
        end = middle - 1
      } else {
        start = middle + 1
      }
    }
  
    targetIndex = start
  
  
    // insert
    intervals.splice(targetIndex, 0, newInterval)
  
    const mergeTwo = (a, b) => {
      return [Math.min(a[0], b[0]), Math.max(a[1], b[1])]
    }

    const isOverlap = (a, b) => {
      return a[1] >= b[0]
    }


    let i = targetIndex
    // O(n)
    while (i < intervals.length) {
      if (i > 0 && isOverlap(intervals[i - 1], intervals[i])) {
        intervals.splice(i - 1, 2, mergeTwo(intervals[i - 1], intervals[i]))
      } else {
        i += 1
      }
    }

    return intervals
};
```
