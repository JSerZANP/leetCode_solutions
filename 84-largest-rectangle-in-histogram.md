Here is the video of me explaining this on youtube: https://youtu.be/YGa6TvkQQKw


```js
/**
 * @param {number[]} heights
 * @return {number}
 */

// brute force one
// O(n^2 * n) => TLE
// var largestRectangleArea = function(heights) {
//     let max = 0
//     for (let i = 0; i < heights.length; i++) {
//         for (let j = i;  j < heights.length; j++) {
//             const min = Math.min(...heights.slice(i, j + 1))
//             max = Math.max(max, min * (j - i + 1))
//         }
//     }
//     return max
// };

// improved brute force
// O(n^2)
// var largestRectangleArea = function(heights) {
//     let max = 0
//     // check ending bar
//     for (let i = 0; i < heights.length; i++) {
//         // check it backwards to get the minimum
//         let smaller = heights[i]
//         for (let j = i; j > -1; j--) {
//             if (heights[j] === 0) break
//             smaller = Math.min(smaller, heights[j])
//             max = Math.max(max, smaller * (i - j + 1))
//         }
//     }
//     return max
// };


// 
var largestRectangleArea = function(heights) {
    let max = 0

    // [index, height]
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

```
