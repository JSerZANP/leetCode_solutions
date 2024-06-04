```js
/**
 * @param {number[][]} points
 * @return {number}
 */
var maxPoints = function (points) {
  // brute force

  // choose two points to determine a line O(N^2)
  // then check other points if they are on it O(N^3)

  // for a point, we constantly check if it blongs to O(N^2) lines
  // is it possible we somehow hash?

  // if we fix a point, we can easily find the longest line
  // by calculating the angles with all other points => O(n)
  // thus improving the algorithm into O(n^2)
  let max = 1;
  for (let i = 0; i < points.length; i++) {
    const tanCount = new Map();
    for (let j = i + 1; j < points.length; j++) {
      let tan = (points[j][1] - points[i][1]) / (points[j][0] - points[i][0]);
      // normalize if Infinity
      if (tan === -Infinity) {
        tan = Infinity;
      }
      const count = (tanCount.get(tan) ?? 0) + 1;
      max = Math.max(max, count + 1);
      tanCount.set(tan, count);
    }
  }
  return max;
};
```
