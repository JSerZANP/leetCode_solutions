Here is a video explaining this  https://youtu.be/pmImer7O3pM


```js
/**
 * @param {number[][]} grid
 * @return {number}
 */
var shortestDistance = function(grid) {
    

// 1 - 11 - 2 - 16 - 1
// |   |   |   |   |
// 11 - 12 - 13 - 14 - 16
// |   |   |   |   |
// 12 - 13 - 1 - 15 - 17
    
    const rows = grid.length
    const cols = grid[0].length
    // mark with [steps, reachableBuildingCount]
    const directions = [[1, 0], [-1, 0], [0, -1],[0, 1]]
    // BFS
    const markSteps = (x, y) => {
        let distance = 0
        const queue = [[x, y]]
        
        const marked = new Array(rows).fill(0).map(_ => new Array(cols).fill(false))
        
        while (queue.length > 0) {
            queue.push(null)
            
            let head;
            while (head = queue.shift()) {
                if (distance !== 0) {
                    // set the distance
                    if (grid[head[0]][head[1]] === 0) {
                        grid[head[0]][head[1]] = [distance, 1]
                    } else {
                        grid[head[0]][head[1]][0] += distance
                        grid[head[0]][head[1]][1] += 1
                    }
                }
                
                // push the next round of empty lands
                for (let direction of directions) {
                    const next = [head[0] + direction[0], head[1] + direction[1]]
                    if (next[0] >= 0 &&  next[0] < rows && next[1] >= 0 && next[1] < cols
                        && grid[next[0]][next[1]] !== 1 &&  grid[next[0]][next[1]] !== 2 && !marked[next[0]][next[1]]) {
                        queue.push(next)
                        marked[next[0]][next[1]] = true
                    }
                }   
            }
            distance += 1
        }
        
    }
    
    let buildingCount = 0
    for (let i = 0; i < grid.length; i++) {
        for (let j = 0; j < grid[i].length; j++) {
           if (grid[i][j] === 1) {
                buildingCount += 1
                markSteps(i, j)
           }
        }
    }
    
    
    let minDistance = Infinity
    
    for (let i = 0; i < grid.length; i++) {
        for (let j = 0; j < grid[i].length; j++) {
           if (Array.isArray(grid[i][j])) {
               const [distance, reachableBuildingCount] = grid[i][j]
               if (reachableBuildingCount === buildingCount) {
                    minDistance = Math.min(minDistance, distance)
               }
           }
        }
    }
    
    return minDistance === Infinity ? -1 : minDistance
};
```
