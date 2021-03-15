me explaining on youtube: https://youtu.be/fWi-eTztTyg
```js
 /**
 * @param {number[][]} grid
 * @return {number}
 */
// Time: < O(n ^ 2)
// space: O(n ^ 2)

// var shortestPathBinaryMatrix = function(grid) {
//     if (grid[0][0] === 1) return -1
//     // use a flag map to store traversed cell
//     const visited = new Set()
    
//     const length = grid.length
    
//     let steps = 1
//     // use a queue to store the cells of certain steps
//     const queue = [[0, 0]]
    
//     // check if a coord is valid
    
//     const isAvailably = ([i, j]) => {
//          const key = `${i}_${j}`
//         if (i < 0 || i >= length || j < 0 || j >= length || grid[i][j] === 1 || visited.has(key)) {
//             return false
//         }
//         return true
//     }
    
//     while (queue.length > 0) {
//         queue.push(null)
//         let head
//         while(head = queue.shift()) {
//             if (head[0] === length - 1 && head[1] === length - 1) {
//                 return steps
//             }
            
//             const key = `${head[0]}_${head[1]}`
//             if (visited.has(key)) {
//                 continue
//             }
//             visited.add(key)
            
//             // push in the next round
//             for (let i = -1; i <=1 ; i++) {
//                 for (let j = -1; j <= 1; j++) {
//                     if (i === 0 && j === 0) continue
//                     const next = [head[0] + i, head[1] + j]
                    
//                     if (isAvailably(next)) {
//                         queue.push(next)
//                     }
//                 }
//             }
//         }
//         steps += 1
//     }
    
//     return -1
// };




// Time: O(n ^ 2)
// Space: O(n ^ 2)
var shortestPathBinaryMatrix = function(grid) {
    if (grid[0][0] === 1) return -1
    // use a flag map to store traversed cell
    
    const length = grid.length
    
    let steps = 1
    // use a queue to store the cells of certain steps
    const queue = [[0, 0]]
    
    // check if a coord is valid
     const isAvailably = ([i, j]) => {
        if (i < 0 || i >= length || j < 0 || j >= length || grid[i][j] === 1) {
            return false
        }
        return true
    }
    
    while (queue.length > 0) {
        queue.push(null)
        let head
        while(head = queue.shift()) {
            if (head[0] === length - 1 && head[1] === length - 1) {
                return steps
            }
            
            // push in the next round
            for (let i = -1; i <=1 ; i++) {
                for (let j = -1; j <= 1; j++) {
                    if (i === 0 && j === 0) continue
                    const next = [head[0] + i, head[1] + j]
                    if (isAvailably(next)) {
                        grid[next[0]][next[1]] = 1
                        queue.push(next)
                    }
                }
            }
    
        }
        steps += 1
    }
    
    return -1
};



 
```
