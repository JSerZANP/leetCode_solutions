Youtube video explanation: https://youtu.be/5Rr25okRNq4


```js
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solveSudoku = function(board) {
    const isUsedInRow = new Array(9).fill(0).map(_ => new Array())
    const isUsedInCol = new Array(9).fill(0).map(_ => new Array())
    const isUsedInSub = new Array(9).fill(0).map(_ => new Array())
    
    for (let i = 0; i < 9; i++) {
      for (let j = 0; j < 9; j++) {
        const num = board[i][j]
        if (num === '.') continue
        const subBoxIndex = Math.floor(i / 3) + Math.floor(j / 3) * 3
        isUsedInRow[i][num] = true
        isUsedInCol[j][num] = true
        isUsedInSub[subBoxIndex][num] = true
      }
    }
  
    // fill the blanks by backtracking
    const fill = (i, j) => {
      if (i === 9) return true
      const nextI = j === 8 ? i + 1 : i
      const nextJ = j < 8 ? j + 1: 0
      const subBoxIndex = Math.floor(i / 3) + Math.floor(j / 3) * 3
      if (board[i][j] === '.') {
        for (let num = 1; num <= 9; num++) {
          if (!isUsedInRow[i][num] && !isUsedInCol[j][num] && !isUsedInSub[subBoxIndex][num]) {
            board[i][j] = `${num}`
            isUsedInRow[i][num] = true
            isUsedInCol[j][num] = true
            isUsedInSub[subBoxIndex][num] = true
            
            if (fill(nextI, nextJ)) {
              return true
            }
            
            // if no number is valid here
            board[i][j] = '.'
            isUsedInRow[i][num] = false
            isUsedInCol[j][num] = false
            isUsedInSub[subBoxIndex][num] = false
          }
        }
        return false
      } else {
        return fill(nextI, nextJ)
      }
    }
    
    fill(0, 0)
};
```
