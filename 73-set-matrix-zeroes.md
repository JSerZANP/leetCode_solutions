Here is a video explaining this: https://youtu.be/cRzlaCj5m1M

```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */

// traverse all the zero
// keep track of the cols and rows that should be set to zero
// update the zeros after traversal
// worst Time: O(mn) + O(mn) + O(mn)
// Space: O(m + n)
// var setZeroes = function(matrix) {
//   const colsOfZero = new Set()
//   const rowsOfZero = new Set()

//   matrix.forEach((row, i) => {
//     row.forEach((item, j) => {
//       if (item === 0) {
//         colsOfZero.add(j)
//         rowsOfZero.add(i)
//       }
//     })
//   })

//   // update the zeros
//   for (let row of rowsOfZero.values()) {
//     for (let j = 0; j < matrix[row].length; j++) {
//       matrix[row][j] = 0
//     }
//   }

//   for (let col of colsOfZero.values()) {
//     for (let i = 0; i < matrix.length; i++) {
//       matrix[i][col] = 0
//     }
//   }
// };

// Recursion, Walker? Vistor?

// 4 times for each cell
// worst Time: O(mm) + O(mn) + 4 * O(mn) = 5O(mn)
// Space: O(1)
var setZeroes = function (matrix) {
  const walk = (i, j, direction) => {
    const [nextI, nextJ] = [i + direction[0], j + direction[1]];
    if (
      nextI >= 0 &&
      nextI < matrix.length &&
      nextJ >= 0 &&
      nextJ < matrix[i].length
    ) {
      if (matrix[nextI][nextJ] === 0) {
        matrix[nextI][nextJ] = undefined;
        walk(nextI, nextJ, [0, 1]);
        walk(nextI, nextJ, [1, 0]);
        walk(nextI, nextJ, [0, -1]);
        walk(nextI, nextJ, [-1, 0]);
      } else if (matrix[nextI][nextJ] === undefined) {
        walk(nextI, nextJ, direction);
      } else {
        matrix[nextI][nextJ] = undefined;
        walk(nextI, nextJ, direction);
      }
    }
  };

  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] === 0) {
        matrix[i][j] = undefined;
        walk(i, j, [0, 1]);
        walk(i, j, [1, 0]);
        walk(i, j, [0, -1]);
        walk(i, j, [-1, 0]);
      }
    }
  }

  for (let i = 0; i < matrix.length; i++) {
    for (let j = 0; j < matrix[i].length; j++) {
      if (matrix[i][j] === undefined) {
        matrix[i][j] = 0;
      }
    }
  }
};
```

Another try

```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var setZeroes = function (matrix) {
  // walk around the cells
  // if we flip the cells into zero, then we are not able to tell if the zero is originall zero
  // we need to store the info somewhere
  // why not store the info at the traversed cells?
  // basically a cell of 0 equals two zeros at the left-most or top-most
  // then in the end, we can just take alook at the first row and first col

  let rows = matrix.length;
  let cols = matrix[0].length;
  let firstRow0 = false;
  let firstCol0 = false;
  for (let i = 0; i < rows; i++) {
    for (let j = 0; j < cols; j++) {
      if (matrix[i][j] === 0) {
        if (i === 0) {
          firstRow0 = true;
        }

        if (j === 0) {
          firstCol0 = true;
        }

        if (i !== 0 && j !== 0) {
          matrix[i][0] = 0;
          matrix[0][j] = 0;
        }
      }
    }
  }
  for (let i = 1; i < rows; i++) {
    for (let j = 1; j < cols; j++) {
      if (matrix[i][0] === 0 || matrix[0][j] === 0) {
        matrix[i][j] = 0;
      }
    }
  }
  if (firstRow0) {
    for (let j = 0; j < cols; j++) {
      matrix[0][j] = 0;
    }
  }

  if (firstCol0) {
    for (let i = 0; i < rows; i++) {
      matrix[i][0] = 0;
    }
  }
};
```
