A video explaining this: https://youtu.be/vPNX6AWiTqA


```js
/**
 * @param {number} n
 * @return {number[][]}
 */
var generateMatrix = function(n) {
   if (n === 0) return []
   if (n === 1) return [[1]]
  
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
   
   const result = Array(n).fill(0).map(item => Array(n).fill(-1))
   
   let i = 0
   let j = 0
   const total = n ** 2
   let count = 1
   
   while (count <= total) {
     result[i][j] = count
     
     // check if we need to turn right
     const nextPossible = [i + directions[currentDirectionIndex][0], j + directions[currentDirectionIndex][1]];
     
     // if it is overflowed, or it is already set, turn right
     if (nextPossible[0] < 0 || nextPossible[0] >= n ||
        nextPossible[1] < 0 || nextPossible[1] >= n ||
        result[nextPossible[0]][nextPossible[1]] !== -1) {
       turnRight()
     }
     
      i += directions[currentDirectionIndex][0]
      j += directions[currentDirectionIndex][1]
     
      count += 1
   }
   
  
  return result
};
```
