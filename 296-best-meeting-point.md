```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var minTotalDistance = function (grid) {
  // brute force
  // O(mnk)

  // but actually we can do better?
  // sinc we are doing manhattan distance
  // suppose we have the best meeting point at (i, j)
  // if we fix i, and move j around
  // we can see that the vertical distance people have to move aren't change

  // so we can actually choose row first, then column

  // this results in O((m + n) * k)

  // even better
  // we can just merge the people for same row into a count.
  // an result in O(m)

  // the pre-caculation is O(m*n)
  // so O(m + n + m*n)
  const m = grid.length;
  const n = grid[0].length;

  const countAtRow = new Array(m).fill(0);
  const countAtCol = new Array(n).fill(0);

  grid.forEach((row, i) => {
    row.forEach((num, j) => {
      if (num === 1) {
        countAtRow[i] += 1;
        countAtCol[j] += 1;
      }
    });
  });

  let minRowDistance = Infinity;
  for (let i = 0; i < m; i++) {
    let distance = 0;
    for (let j = 0; j < m; j++) {
      distance += countAtRow[j] * Math.abs(j - i);
    }
    if (distance < minRowDistance) {
      minRowDistance = distance;
    }
  }

  let minColDistance = Infinity;
  for (let i = 0; i < n; i++) {
    let distance = 0;
    for (let j = 0; j < n; j++) {
      distance += countAtCol[j] * Math.abs(j - i);
    }
    if (distance < minColDistance) {
      minColDistance = distance;
    }
  }

  return minRowDistance + minColDistance;
};
```
