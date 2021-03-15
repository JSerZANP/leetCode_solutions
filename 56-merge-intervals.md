Youtube explaining this: https://youtu.be/58Mourc9grM

```js
var merge = (intervals) => {
  const isOverlapping = (interval1, interval2) => {
    if (interval1[0] > interval2[1] || interval1[1] < interval2[0]) {
      return false
    }
    return true
  }
  
  const merge2 = (interval1, interval2) => {
    // [1,3] + [2,4] => [1, 4]
    interval2[0] = Math.min(interval1[0], interval2[0])
    interval2[1] = Math.max(interval1[1], interval2[1])
  }
  
  intervals.sort((a, b) => a[0] - b[0])
  let result = []
  
  for (let i = 0; i < intervals.length; i++) {
    const head = intervals[i]
    const top = result[result.length - 1]
    if (top && isOverlapping(top, head)) {
      merge2(head, top)
    } else {
      result.push(head)
    } 
  }
  
  return result
}
```
