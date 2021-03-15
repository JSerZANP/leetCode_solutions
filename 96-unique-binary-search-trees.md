me explaining this on youtube: https://youtu.be/TWPcEDt8Mtg

```js
/**
 * @param {number} n
 * @return {number}
 */

// recursion solution
// Time: f(n) = Catalan(n) Catalan Number
// Catalan(n) = (2n)C(n) / (n + 1)

// var numTrees = function(n) {
//     if (n <= 1) return 1
    
//     let count = 0
//     for (let i = 1; i <= n; i++) {
//         count += numTrees(i - 1) * numTrees(n - i)
//     }
    
//     return count
// };


// memoization
const cache = new Map()
var numTrees = function(n) {
    if (cache.has(n)) return cache.get(n)
    
    if (n <= 1) return 1

    let count = 0
    for (let i = 1; i <= n; i++) {
        count += numTrees(i - 1) * numTrees(n - i)
    }
    
    cache.set(n, count)
    return count
}
```
