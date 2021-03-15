Youtube video explaining this: https://youtu.be/jJjaRfQLoTw

```js
/**
 * @param {number[][]} grid
 * @param {number} r0
 * @param {number} c0
 * @param {number} color
 * @return {number[][]}
 */
var colorBorder = function(grid, r0, c0, color) {
    // same as a problem we did before
    // push possible cell in to a tempary array
    let arr = [[r0, c0]];
  
    const row = new Array(grid[0].length).fill(0);
    const checked = new Array(grid.length).fill(0).map(item => row.slice(0));
    checked[r0][c0] = 1;
    const rows = grid.length;
    const columns = grid[0].length;
    const initColor = grid[r0][c0];
    while (arr.length > 0) {
      const nextArr = []
      for (let i = 0, total = arr.length; i < total; i++) {
        const cell = arr[i];
        if (cell[0] === 0 || cell[0] === rows - 1 || cell[1] === 0 || cell[1] === columns - 1 ||
           grid[cell[0] + 1][cell[1]] !== initColor ||
           grid[cell[0] - 1][cell[1]] !== initColor ||
           grid[cell[0]][cell[1] + 1] !== initColor ||
           grid[cell[0]][cell[1] - 1] !== initColor ) {
          checked[cell[0]][cell[1]] = 2;
        }
        
        
        if (cell[0] + 1 < rows && checked[cell[0] + 1][cell[1]] === 0 && grid[cell[0] + 1][cell[1]] === initColor) {
          checked[cell[0] + 1][cell[1]] = 1;
          nextArr.push([cell[0] + 1, cell[1]]);
        }
        
        if (cell[0] - 1 > -1 && checked[cell[0] - 1][cell[1]] === 0 && grid[cell[0] - 1][cell[1]] === initColor) {
          checked[cell[0] - 1][cell[1]] = 1;
          nextArr.push([cell[0] - 1, cell[1]]);
        }
                       
        if (cell[1] + 1 < columns && checked[cell[0]][cell[1] + 1] === 0 && grid[cell[0]][cell[1] + 1] === initColor) {
          checked[cell[0]][cell[1] + 1] = 1;
          nextArr.push([cell[0], cell[1] + 1]);
        }
                       
        if (cell[1] - 1 > -1 && checked[cell[0]][cell[1] - 1] === 0 && grid[cell[0]][cell[1] - 1] === initColor) {
          checked[cell[0] ][cell[1]- 1] = 1;
          nextArr.push([cell[0], cell[1] - 1]);
        }
      }
      arr = nextArr;
    }
    
    checked.forEach((row, i) => {
        row.forEach((cell, j) => {
            if (cell === 2) {
                grid[i][j] = color
            }
        })
    })
    return grid;
};
```
