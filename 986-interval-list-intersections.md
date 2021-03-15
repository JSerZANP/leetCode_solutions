me explaining this on youtube: https://youtu.be/zLSGHhE8Tug

```js
/**
 * @param {number[][]} A
 * @param {number[][]} B
 * @return {number[][]}
 */

// Time: O(m + n)
// Space: O(1)
var intervalIntersection = function(A, B) {
  
    const getIntersection = (a, b) => {
      if (a[1] < b[0] || b[1] < a[0]) return null
      return [Math.max(a[0], b[0]), Math.min(a[1], b[1])]
    }
  
    const result = []
    // get intersection and shift the heads(smaller)
  
    
    while (A.length > 0  && B.length > 0) {
      const a = A[0]
      const b = B[0]
      
      const intersection = getIntersection(a, b)
      
      if (intersection) {
        result.push(intersection)
      }
      
      // shift the interval with smaller right border
      if (A[0][1] <= B[0][1]) {
        A.shift()
      } else {
        B.shift()
      }
    }
  
  
    return result
};
```
