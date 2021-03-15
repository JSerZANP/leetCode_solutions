Here is my youtube video explaining it: https://youtu.be/lvKfbNt5EII


```js
/**
 * @param {number} h
 * @param {number} w
 * @param {number[]} horizontalCuts
 * @param {number[]} verticalCuts
 * @return {number}
 */
// Time: O(nlogn)
// space: O(1)
var maxArea = function(h, w, horizontalCuts, verticalCuts) { // both at length n
    // O(nlogn)
    horizontalCuts.sort((a, b) => a - b)
    // O(nlogn)
    verticalCuts.sort((a, b) => a - b)
  
    horizontalCuts.push(h)
    verticalCuts.push(w)
  
    let maxH = 0
    let prev = 0
    // O(n)
    for (let cut of horizontalCuts) {
      maxH = Math.max(maxH, cut - prev)
      prev = cut
    }
  
    let maxV = 0
    prev = 0
    // O(n)
    for (let cut of verticalCuts) {
      maxV = Math.max(maxV, cut - prev)
      prev = cut
    }
  
    return (maxH * maxV) % (10 ** 9 + 7)
};
```
