Here is the video explaining this: https://youtu.be/zGSP9I0_oJs

```js
/**
 * @param {number[][]} rooms
 * @return {void} Do not return anything, modify rooms in-place instead.
 */

// BFS
// time: O(mn, )

// supoose k 0, take up mn/k areas 
//  mn + k * mn/k => O(mn)

// => O(mn)
// Space: O(1)
var wallsAndGates = function(rooms) {
    const rows = rooms.length
    if (rows === 0) return
  
    const cols = rooms[0].length
    if (cols === 0) return
    
    
    const walk = (i, j, distance) => {
      // Array<[x, y, distance]>
      const queue = [[i, j, distance]]
      
      let head
      while (head = queue.shift()) {
        const [i, j, distance] = head
        if (rooms[i][j] > distance || rooms[i][j] === 0) {
          rooms[i][j] = distance
          
          const nextDistance = distance + 1
          // push the next possible coordinates in
          if (i > 0 && rooms[i - 1][j] > nextDistance) {
            queue.push([i - 1, j, nextDistance])
          }
          
          if (i + 1 < rows && rooms[i + 1][j] > nextDistance) {
            queue.push([i + 1, j, nextDistance])
          }
          
          if (j > 0 && rooms[i][j - 1] > nextDistance) {
            queue.push([i, j - 1, nextDistance])
          }
          
          if (j + 1 < cols && rooms[i][j + 1] > nextDistance) {
            queue.push([i, j + 1, nextDistance])
          }
        }
      }
    }
    
  
    for (let i = 0; i < rows; i++) {
      for (let j = 0; j < cols; j++) {
        if (rooms[i][j] === 0) {
          walk(i, j, 0)
        }
      }
    }
  
    return rooms
};
```
