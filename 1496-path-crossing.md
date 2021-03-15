A video of this: https://youtu.be/NnlbI98AkCM

```js
/**
 * @param {string} path
 * @return {boolean}
 */
var isPathCrossing = function(path) {
    // use a set to keep track of the walked points
    // once found crossed, return immediately
    
    const directions = {
      N: [0, 1],
      E: [1, 0],
      S: [0, -1],
      W: [-1, 0]
    }
    // Set<string>
    const walked = new Set()
    let currentCoord = null
    
    const walk = (point) => {
      const key = point.join('_')
      if (walked.has(key)) {
        return true
      }
      walked.add(point.join('_'))
      currentCoord = point
      return false
    }
    
    walk([0, 0])
  
    for (let step of path) {
      const direction = directions[step]
      const next = [currentCoord[0] + direction[0], currentCoord[1] + direction[1]]
      if (walk(next)) {
        return true
      }
    }
  
    return false
};
```
