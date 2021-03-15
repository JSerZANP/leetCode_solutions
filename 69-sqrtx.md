
Here is a video explaining this: https://youtu.be/xoeMhTvg11M

```js
/**
 * @param {number} x
 * @return {number}
 */
// var mySqrt = function(x) {
//     // 0 1 2 .... x
//     // pick the number, that square of it right equal/smaller than x
//     // binary search
  
//     // O(log(x))
    
//     let i = 0
//     let j = x
    
//     // [i, middle, j]
//     while (i < j) {
//       const middle = Math.ceil((i + j) / 2) // means if i === j - 1, middle would be j
//       const square = middle ** 2
//       if (square === x) return middle
//       if (square < x) {
//         i = middle
//       } else {
//         j = middle - 1
//       }
//     }
  
//     return i
// };

var mySqrt = function(x) {
    if (x < 2) return x
    // 0 1 2 .... x
    // pick the number, that square of it right equal/smaller than x
    // binary search
  
    // O(log(x))
    let i = 0
    let j = x
    
    // [i, middle, j]
    while (i < j) {
      const middle = Math.floor((i + j) / 2) // means if i === j - 1, middle would be i
      const square = middle ** 2
      if (square === x) return middle
      if (square < x) {
        i = middle + 1
      } else {
        j = middle
      }
    }
  
    return j - 1
};
```
