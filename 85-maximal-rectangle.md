Here is my video explaining it on youtube: https://youtu.be/O6S3xNDdAYw

```js
/**
 * @param {character[][]} matrix
 * @return {number}
 */
// brute force with m * n
// C(m*n, 2) / 2 =

// Top 3 row
// [3, 1, 3, 2, 2] for No.84

// Top 4 rows
// [4, 0. 0, 3, 0] for No.84


// [4, 0, 0, 3,  0]


var largestRectangleArea = function(heights) {
    let max = 0

    // [index, height]
    // [1,2,2,2,2,3,3]
    let keypoints = [[-1, 0]]
    
    const crush = (index, height) => {
        const newPoint = [index, height]
        if (keypoints[keypoints.length - 1][1] >= height) {
            // crush the right-most keypoint if it is not smaller
            while (keypoints.length > 1 && keypoints[keypoints.length - 1][1] >= height) {
                const top = keypoints.pop()
                max = Math.max(max, top[1] * (index - top[0]))
                newPoint[0] = top[0]
            }
        
        }
        
        keypoints.push(newPoint)
    }
    
    for (let i = 0; i < heights.length; i++) {
        crush(i, heights[i])
    }
    
    crush(heights.length, 0)
    
    return max
};


// O(n^2)
var maximalRectangle = function(matrix) {
    if (matrix.length === 0) return 0
    
    let result = 0
    
    const count = matrix[0].map(_ => 0)
    
    // n
    matrix.forEach((row, i) => {
        // n
        for (let j = 0; j < count.length; j++) {
            if (row[j] === '0') {
                count[j] = 0
            } else {
                count[j] += 1
            }
        }
        
        // n
        result = Math.max(result, largestRectangleArea(count))
    })
    
    return result
};
```
