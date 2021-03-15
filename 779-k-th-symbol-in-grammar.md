A video explaining this: https://youtu.be/jL39TzQ7HHo


```js
/**
 * @param {number} N
 * @param {number} K
 * @return {number}
 */

// Recursion
// Time O(N)
// Space O(N)
// var kthGrammar = function(N, K) {
//     if (N === 1) {
//       return 0
//     }
//     const prevK = Math.ceil(K / 2)
//     if (K % 2 === 0) {
//       return (kthGrammar(N - 1, prevK) + 1)  % 2
//     } else {
//       return kthGrammar(N - 1, prevK)
//     }
// };

// Tail Recursion
// Time O(N)
// Space O(1)
var kthGrammar = function(N, K) {
  
    const _kthGrammer = (N, K, carrier) => {
      if (N === 1) {
        return (0 + carrier) % 2
      }
      const prevK = Math.ceil(K / 2)
      return _kthGrammer(N - 1, prevK, carrier + (K % 2 === 0 ? 1 : 0))
    }
  
    return _kthGrammer(N, K, 0)
};
```
