A video explaining this: https://youtu.be/mJIYFfrdWZ0

```js
/**
 * @param {number[]} A
 * @param {number[]} B
 * @return {number}
 */
var findLength = function(A, B) {
    let max = 0;

    let matrix = new Array(A.length)
    for (let i = 0; i < A.length; i++) {
        matrix[i] = new Array(B.length)
        for(let j = 0; j < B.length; j++) {
            if (i === 0 || j === 0) {
                matrix[i][j] = A[i] === B[j]  ? 1 : 0
            } else {
                matrix[i][j] = A[i] === B[j] ? matrix[i - 1][j - 1] + 1 : 0
            }
            
            if (matrix[i][j] > max) {
                max = matrix[i][j]
            }
        }
    }
    return max
};
```
