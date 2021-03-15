Me explaining it on youtube: https://youtu.be/6GgZbjcBCEk

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @param {number} x
 * @return {number[]}
 */

// Time: O(log N) + k^2
var findClosestElements = function(arr, k, x) {
    // find the position o x, and expand in two directions
  
    // [, 3] => 3
    // [-Infinity, 1] => -1
  
    // binary search
    arr.unshift(-Infinity)
    arr.push(Infinity)
  
    let i = 0;
    let j = arr.length
    
    while (j - i > 1) {
      const middle = Math.floor((i + j) / 2)
      if (arr[middle] === x) {
        i = middle - 1
        j = middle
        break
      } else if (arr[middle] < x) {
        i = middle
      } else {
        j = middle
      }
    }
  
    // now get [i, j] which x is at j, or right before j
    let count = 0
    while (count < k) {
      if (Math.abs(arr[i] - x) <= Math.abs(arr[j] - x)) {
        i -= 1
      } else {
        j += 1
      }
      count += 1
    }
  
    return arr.slice(i + 1, j)
};
  
  
  
  
  
  
  ```
