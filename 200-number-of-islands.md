Here is a video explaining it: https://youtu.be/ImqyM7_R70E


```js
/**
 * @param {character[][]} grid
 * @return {number}
 */
var numIslands = function(grid) {
   // 1. step on one 1, start search for connected points (walk)
   // 2. use a 2d array to mark a pointed being walked on
   // 3. count the step 1
    
   const rows = grid.length
   if (rows === 0) return 0
   const cols = grid[0].length
   
   const directions = [
     [0, 1],
     [0, -1],
     [1, 0],
     [-1, 0]
   ]
   
   const walked = new Array(rows).fill(0).map(_ => new Array(cols).fill(false))
   
   let result = 0
     
   const walk = (row, col) => {
     result += 1
     
     const stack = [[row, col]]
     walked[row][col] = true
     
     while (stack.length > 0) {
        const top = stack.pop()
        for (let direction of directions) {
          const next = [top[0] + direction[0], top[1] + direction[1]]
          if (
            next[0] > -1 && next[0] < rows &&
            next[1] > -1 && next[1] < cols && 
            grid[next[0]][next[1]] === '1' && !walked[next[0]][next[1]]) {
            stack.push(next)
            walked[next[0]][next[1]] = true
          }
        }
     }
   }
   
   for (let row = 0; row < rows; row++) {
     for (let col = 0; col < cols; col++) {
       // if it is land and not walked before
       if (grid[row][col] === '1' && !walked[row][col]) {
         walk(row, col)
       }
     }
   }
  
   return result
};
```
