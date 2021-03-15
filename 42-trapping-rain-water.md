Youtube video explaining this: https://youtu.be/LyuDZSNHn48


```js
/**
 * @param {number[]} height
 * @return {number}
 */
var trap = function(height) {
    const maxFromLeft = new Array(height.length).fill(0)
    const maxFromRight = new Array(height.length).fill(0)
    
    let max = 0
    for (let i = 0; i < height.length; i++) {
      max = Math.max(height[i], max)
      maxFromLeft[i] = max
    }
  
    max = 0
    for (let i = height.length - 1; i > -1; i--) {
      max = Math.max(height[i], max)
      maxFromRight[i] = max
    }
  
    let maxWater = 0
    for (let i = 0; i < height.length; i++) {
      const boundary = Math.min(maxFromLeft[i], maxFromRight[i])
      maxWater += boundary - height[i]
    }
  
    return maxWater
};
```
