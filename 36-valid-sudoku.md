A video explaining this: https://youtu.be/1-6VjaJg2pM

```js
/**
 * @param {character[][]} board
 * @return {boolean}
 */


// Brute Force, with 3 passes   9 * 9 * 3

// let's improve it to 1 pass
var isValidSudoku = function(board) {
    const isUsedInRow = new Array(9).fill(0).map(_ => new Array())
    const isUsedInCol = new Array(9).fill(0).map(_ => new Array())
    const isUsedInSub = new Array(9).fill(0).map(_ => new Array())
    
    for (let i = 0; i < 9; i++) {
      for (let j = 0; j < 9; j++) {
        const num = board[i][j]
        if (num === '.') continue
        const subBoxIndex = Math.floor(i / 3) + Math.floor(j / 3) * 3
        if (isUsedInRow[i][num] || isUsedInCol[j][num] || isUsedInSub[subBoxIndex][num]) {
          return false
        }
        isUsedInRow[i][num] = true
        isUsedInCol[j][num] = true
        isUsedInSub[subBoxIndex][num] = true
      }
    }
  
    return true
};
```
