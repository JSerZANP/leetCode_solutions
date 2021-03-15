Youtube video explaining this: https://youtu.be/xwl9bgV3NJo


```js
/**
 * @param {number} R
 * @param {number} C
 * @param {number} r0
 * @param {number} c0
 * @return {number[][]}
 */
const getNextRoundPoints = (R, C, mapChecked, x, y) => {
       const result = [];
       if (x - 1 >= 0 && mapChecked[x - 1][y] === 0) {
         result.push([x - 1, y])
         mapChecked[x - 1][y] = 1
       }
       if (y - 1 >= 0 && mapChecked[x][y - 1] === 0) {
         result.push([x, y - 1])
         mapChecked[x][y - 1] = 1
       }
       if (x + 1 <= R - 1 && mapChecked[x + 1][y] === 0) {
         result.push([x + 1, y])
         mapChecked[x + 1][y] = 1
       }
  
       if (y + 1 <= C - 1 && mapChecked[x][y + 1] === 0) {
         result.push([x, y + 1])
         mapChecked[x][y + 1] = 1
       }
  
       return result;
}

var allCellsDistOrder = function(R, C, r0, c0) {
     // x x x x
     // x x x x
     // x x O x
     // x x x x
     const mapChecked = [];
     for (let i = 0; i < R; i++) {
       const row = [];
       for (let j = 0; j < C; j++) {
         row.push(0);
       }
       mapChecked.push(row);
     }
     
     let result = [];
     let pointsAtCurrentRound = [[r0, c0]];
     mapChecked[r0][c0] = 1;
     
     while (pointsAtCurrentRound.length > 0) {
       result = result.concat(pointsAtCurrentRound);
       let nextPoints = [];
       pointsAtCurrentRound.forEach(point => {
         nextPoints = nextPoints.concat(getNextRoundPoints(R, C, mapChecked, point[0], point[1]));
       })
       
       pointsAtCurrentRound = nextPoints;
     }
     return result;
};
```
