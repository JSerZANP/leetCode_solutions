```js
/**
 * @param {number[][]} board
 * @return {number}
 */
var snakesAndLadders = function (board) {
  // shortest path, BFS search

  const size = board.length;
  const visited = new Set();

  const queue = [1];
  let step = 0;
  while (queue.length > 0) {
    let count = queue.length;
    while (count > 0) {
      const head = queue.shift();
      if (!visited.has(head)) {
        visited.add(head);
        if (head === size ** 2) return step;
        for (let j = head + 1; j <= Math.min(head + 6, size ** 2); j++) {
          const [row, col] = getCoordFromLabel(j, size);
          if (board[row][col] === -1) {
            queue.push(j);
          } else {
            // // it might be connected so we need repeat the search
            // let path = new Set([j])
            let p = board[row][col];
            // console.log('got snake/ladder at', j, ' to ', p)
            // while (!path.has(p)) {
            //     const [row, col] = getCoordFromLabel(p, size)
            //     if (board[row][col] === -1) {
            //         break
            //     } else {
            //         console.log('got snake/ladder at', p, ' to ', board[row][col])
            //         path.add(p)
            //         p = board[row][col]
            //     }
            // }
            // console.log('p stops at', p)
            // // p stops at the last position
            // // or at a circle
            // // circle means dead end
            // if (!path.has(p)) {
            queue.push(p);
            // }
          }
        }
      }
      count -= 1;
    }
    step += 1;
  }
  return -1;
};

function getCoordFromLabel(i, size) {
  const rowFromBottom = Math.floor((i - 1) / size);
  const row = size - 1 - rowFromBottom;
  const colFromLeft = (i - 1) % size;
  const col = rowFromBottom % 2 === 0 ? colFromLeft : size - 1 - colFromLeft;
  return [row, col];
}

// 7(1) 8(1) 9
// 6(1) 5(1) 4(1)
// 1 2(1) 3(1)
```
