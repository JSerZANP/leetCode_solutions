My video of explaining it: https://youtu.be/jeLs8uS7gCg

```js
/**
 * @param {character[][]} board
 * @return {number}
 */

// Time: O(mn)
// Space: O(max(m, n)) + inline modification
// var countBattleships = function(board) {
//     // loop through all the board => mark as checkded ('')
//     // if found battleship, continue marking connected X , count 1 
//     const rows = board.length
//     const cols = board[0].length
    
//     let count = 0
    
//     // use this flag to mark continuous checking of X
//     const walk = (row, col, isPrevX) => {
//       switch (board[row][col]) {
//         // if checked already
//         case '':
//           return;
//         case '.':
//           board[row][col] = ''
//           return
//         case 'X':
//           if (!isPrevX) count += 1
          
//           if (row + 1 < rows && board[row + 1][col] === 'X') {
//             walk(row + 1, col, true)
//           }
          
//           if (col + 1 < cols && board[row][col + 1] === 'X') {
//             walk(row, col + 1, true)
//           }
        
//           board[row][col] = ''
//       }
//     }
    
//     // loop through all the board
//     for (let row = 0; row < rows; row++) {
//       for (let col = 0; col < cols; col++) {
//         walk(row, col, false)
//       }
//     }
  
//     return count
// };

// to remove inline modification
var countBattleships = function(board) {
   // look at the example
   // simple form (one row)
   // X..X..  => 2
   // .xx.x.  => 2
   // ....x.  => 1 -> 0
  
   // check battleship' head count
   // rule => i, j is head if  [i- 1, j] and [i, j - 1] is not X
   let count = 0
   const rows = board.length
   const cols = board[0].length
   for (let row = 0; row < rows; row++) {
     for (let col = 0; col < cols; col++) {
       if (board[row][col] === 'X' && 
          (col === 0 || board[row][col - 1] !== 'X') &&
          (row === rows - 1 || board[row + 1][col] !== 'X')
          ) {
         count += 1
       }
     }
   }
   return count
};










```
