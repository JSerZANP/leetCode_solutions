Youtube video explaining this: https://youtu.be/95zEFgS4WSo


```js
/**
 * @param {number[][]} matrix
 * @return {number[]}
 */
var spiralOrder = function(matrix) {
  if (matrix.length === 0 || matrix[0].length === 0) return []
  
   const directions = [
     [0, 1],
     [1, 0],
     [0, -1],
     [-1, 0],
    ]
   
   let currentDirectionIndex = 0
   
   const turnRight = () => {
     currentDirectionIndex = (currentDirectionIndex + 1) % directions.length
   }
   
   const result = []
   
   let i = 0
   let j = 0
   const total = matrix.length * matrix[0].length
   
   while (result.length < total) {
     result.push(matrix[i][j])
     matrix[i][j] = null
     
     // check if we need to turn right
     const nextPossible = [i + directions[currentDirectionIndex][0], j + directions[currentDirectionIndex][1]];
     
     // if it is overflowed, or it is traversed, turn right
     if (nextPossible[0] < 0 || nextPossible[0] >= matrix.length ||
        nextPossible[1] < 0 || nextPossible[1] >= matrix[0].length ||
        matrix[nextPossible[0]][nextPossible[1]] === null) {
       turnRight()
     }
     
      i += directions[currentDirectionIndex][0]
      j += directions[currentDirectionIndex][1]
   }
   
  
  return result
};
```
