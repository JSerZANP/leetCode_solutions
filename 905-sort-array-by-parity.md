A video explaining this: https://youtu.be/9VRcShmQoe0
```js
/**
 * @param {number[]} A
 * @return {number[]}
 */

// Time: O(n)
var sortArrayByParity = function(A) {
    // [3,1,2,4]
    // [4,1,2,3]
    // [4,2,1,3]
  
    // [3,1,2,5]
    // [2,1,3,5]
  
    let left = 0
    let right = A.length - 1
    
    while (left < right) {
      // move left to the first odd number
      // move right to the last even number
      while(left < A.length && A[left] % 2 === 0) {
        left += 1
      }
      
      while (right > -1 && A[right] % 2 === 1) {
        right -= 1
      }
      
      if (left < right) {
        [A[left], A[right]] = [A[right], A[left]]
        left += 1
        right -= 1
      }
    }
  
    return A
};
```
