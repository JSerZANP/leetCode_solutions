Here is my video explaining it: https://youtu.be/-A1kGZo6hXs


```js
/**
 * @param {number} steps
 * @param {number} arrLen
 * @return {number}
 */

// naive recursin
// Time: O(3 ^ n)
// Space: O(n)
// var numWays = function(steps, arrLen) {
//     // O O O
//     const walk = (n, i) => {
//         if (i < 0 || i > arrLen - 1) return 0
//         if (n === 0) {
//             return i === 0 ? 1 : 0
//         }
        
//         return walk(n - 1, i) + walk(n - 1, i - 1) + walk(n - 1, i + 1)
//     }
    
//     return walk(steps, 0)
// };


// memoization
// Time: O(steps * arrLen)
// Space: O(steps * arrLen)
// var numWays = function(steps, arrLen) {
//     const max = 10**9 + 7
//     const cache = new Map()
//     const len = Math.min(arrLen, Math.floor(steps / 2) + 1)
//     // O O O
//     const walk = (n, i) => {
//         const key = `${n}_${i}`
        
//         if (cache.has(key)) return cache.get(key)
        
//         if (i < 0 || i > Math.min(n + 1, len) - 1) {
//             cache.set(key, 0)
//             return 0
//         }
        
//         if (n === 0) {
//             const result = i === 0 ? 1 : 0
//             cache.set(key, result)
//             return result
//         }
        
//         const result = (walk(n - 1, i) + walk(n - 1, i - 1) + walk(n - 1, i + 1)) % max
//         cache.set(key, result)
//         return result
//     }
    
//     return walk(steps, 0)
// };


// Time: O(steps * arrLen)
// Space: O(arrLen)
var numWays = function(steps, arrLen) {
    const max = 10**9 + 7
    const len = Math.min(Math.floor(steps / 2) + 1, arrLen)
    let nums = Array(len).fill(0)
    nums[0] = 1
    
    for (let i = 1; i <= steps; i++) {
        const newNums = nums.slice(0)
        
        for (let j = 0; j < Math.min(i + 1, len); j++) {
            newNums[j] = (nums[j] + (nums[j - 1] || 0) + (nums[j + 1] || 0) ) % max
        }
        
        nums = newNums
    }
    
    return nums[0]
}



```
