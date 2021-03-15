me explaining this on youtube: https://youtu.be/l6YuInru5tg

```js
/**
 * @param {number} x
 * @param {number} y
 * @return {number}
 */
var minKnightMoves = function(x, y) {
    // normalize the input
    
    x = Math.abs(x)
    y = Math.abs(y)
    
    
    // use a map to keep track of the visted or not
    const visited = new Map()
    
    const directions = [
        [2, 1],
        [1, 2],
        [-1, 2],
        [-2, 1],
        [-2, -1],
        [-1, -2],
        [1, -2],
        [2, -1]
    ]
    
    // do iteration on each step
    // keep track of the cells , which could be lead to be n-th step
    
    const queue = [[0, 0]]
    
    let step = 0
    // check n-th round points, then push in next round
    while (true) {
        queue.push(null) // as an ending identifier
        
        let head 
        while (head = queue.shift()) {
            const key = `${head[0]}_${head[1]}`
            if (visited.has(key)) continue
            
            visited.set(key, true)
            
            // if it is target?
            if (head[0] === x && head[1] === y) {
                return step
            }
            
            // process next round
            for (let direction of directions) {
                const next = [head[0] + direction[0], head[1] + direction[1]]
                
                // only push in the unvisited && postive ones
                if (!visited.has(`${next[0]}_${next[1]}`) && (step < 2 || (next[0] >= 0 && next[1] >= 0))) {
                    queue.push(next)
                }
            } 
        }
        
        step += 1
    }
};
```
