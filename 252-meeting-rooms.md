Here is a video explaining it : https://youtu.be/Qd7LaGypkS0


```js
/**
 * @param {number[][]} intervals
 * @return {boolean}
 */

// Time: O(nlogn + n) => O(nlogn)
// space: O(1)
var canAttendMeetings = function(intervals) {
    // [   ]     [    ]
    //    [   ]    []
  
    // 1. sort first
    // 2. loop though the intervals and check against previous one (adjasent interval)
  
    const isOverlapping = (interval1, interval2) => {
      return !(interval1[1] <= interval2[0] || interval1[0] >= interval2[1])
    }
    
    intervals.sort((a, b) => a[0] - b[0])
  
    for (let i = 1; i < intervals.length; i++) {
      if (isOverlapping(intervals[i], intervals[i - 1])) {
        return false
      }
    }
    
    return true
};
```
