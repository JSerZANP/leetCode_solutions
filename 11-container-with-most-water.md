A video explaining this: https://youtu.be/ObUUdpIk3hM

```js
/**
 * @param {number[]} height
 * @return {number}
 */

// brute force
// O(n^2)
// var maxArea = function(height) {
//     let max = 0
    
//     for (let i = 0; i < height.length - 1; i++) {
//       for (let j = i + 1; j < height.length; j++) {
//         max = Math.max(max, (j - i) * Math.min(height[i], height[j]))
//       }
//     }
  
//     return max
// };

// two cursors
// O(N)

var maxArea = function(height) {
    let max = 0
    
    let i = 0
    let j = height.length - 1
    
    while (i < j) {
      max = Math.max(max, (j - i) * Math.min(height[i], height[j]))
      
      // try to move the cursors
      if (height[i] < height[j]) {
        // move i to the next bigger border
        let k = i + 1
        while (height[k] <= height[i]) {
          k += 1
        }
        
        i = k
      } else {
        let k = j -  1
        while (height[k] <= height[j]) {
          k -= 1
        }
        
        j = k
      }
    }
  
    return max
};
```
