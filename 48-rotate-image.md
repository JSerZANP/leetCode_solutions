A video explaining this: https://youtu.be/-famaCHwEyI


```js
/**
 * @param {number[][]} matrix
 * @return {void} Do not return anything, modify matrix in-place instead.
 */
var rotate = function(matrix) {
    let depth = 0
    const maxDepth = Math.floor(matrix.length / 2)
    
    while (depth < maxDepth) {
      const length = matrix.length - depth * 2
      const left = depth
      const top = depth
      
      for (let i = 0; i < length - 1; i++) {
        let first = matrix[top][left + i]
        let next = matrix[top + i][left + length - 1]
        
        matrix[top + i][left + length - 1] = first
        
        first = next
        next = matrix[top + length - 1][left + length - 1 - i]
        
        matrix[top + length - 1][left + length - 1 - i] = first
        
        first = next
        next = matrix[top + length - 1 - i][left]
        
        matrix[top + length - 1 - i][left] = first
        
        matrix[top][left + i] = next 
      }
      
      
      depth += 1
    }
};
```
