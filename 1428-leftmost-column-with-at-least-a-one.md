Me explainig it on youtube: https://youtu.be/E4ryrRnuWvY


```js
/**
 * // This is the BinaryMatrix's API interface.
 * // You should not implement it, or speculate about its implementation
 * function BinaryMatrix() {
 *     @param {integer} row, col
 *     @return {integer}
 *     this.get = function(row, col) {
 *         ...
 *     };
 *
 *     @return {[integer, integer]}
 *     this.dimensions = function() {
 *         ...
 *     };
 * };
 */

/**
 * @param {BinaryMatrix} binaryMatrix
 * @return {number}
 */

// Time: O(mlogn)
// Space: O(1)
var leftMostColumnWithOne = function(binaryMatrix) {
    // binary search for 1st 1 in each row
    // narrow it down
    
    const [rows, cols] = binaryMatrix.dimensions()
    
    // return the index, or -1
    const getFirstIndexOf1 = (row, end) => {
      let start = 0
      
      while (start <= end) {
        const middle = Math.floor((start + end) / 2)
        const num = binaryMatrix.get(row, middle)
        if (num === 1) {
          end = middle - 1
        } else {
          start = middle + 1
        }
      }
      
      return binaryMatrix.get(row, start) === 1 ? start : -1
    }
    
    let result = -1
    
    let end = cols - 1
    
    for (let i = 0; i < rows; i++) {
      
      const indexOf1 = getFirstIndexOf1(i, end)
      if (indexOf1 > -1) {
        if (indexOf1 === 0) {
          return 0
        }
        
        result = indexOf1
        end = indexOf1 - 1
      }
    }
  
    return result
};

         
         
         
         
         
         
         
         
```
