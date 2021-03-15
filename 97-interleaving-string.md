
Here is a video for this: https://youtu.be/8vmESAv3vEY

```js
/**
 * @param {string} s1
 * @param {string} s2
 * @param {string} s3
 * @return {boolean}
 */
// Time:  'aaa', 'aaa' 'aaaaaa'
// f(n , n) = f(n-1, n)  + f(n, m -1)
//     = f(n-2, n) + f(n-1, n -1) + f(n -1, n- 1) + f(n, n-2)
//     = 2(f(n-1, n-1) + f(n, n-2))
//     < 4(f(n-1, n-1)
//     =4^N
      
// Space: O(n)
// var isInterleave = function(s1, s2, s3) {
//     if (s1.length + s2.length !== s3.length) return false
//     const walk = (i, j, k) => {
//         if (k === s3.length) return true
        
//         if (i === s1.length && j === s2.length) {
//             return k === s3.length
//         }
        
//         return (s1[i] === s3[k] && walk(i + 1, j, k + 1)) || 
//             (s2[j] === s3[k] && walk(i, j + 1, k + 1))
//     }
    
//     return walk(0,0,0)
// };


// meoization  O(N ^2)
// space: O(N ^ 2) + O(N)
// var isInterleave = function(s1, s2, s3) {
//     if (s1.length + s2.length !== s3.length) return false
//     const cache = new Map()
//     const walk = (i, j, k) => {
//         if (k === s3.length) return true
        
//         const key = `${i}_${j}`
//         if (cache.has(key)) return cache.get(key)
        
//         if (i === s1.length && j === s2.length) {
//             return k === s3.length
//         }
        
//         const result = (s1[i] === s3[k] && walk(i + 1, j, k + 1)) || 
//             (s2[j] === s3[k] && walk(i, j + 1, k + 1))
//         cache.set(key, result)
//         return result
//     }
    
//     return walk(0,0,0)
// };

      
// s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
// f(i, j) = {
//        f(i - 1, j) if s1's end matches
//        f(i, j - 1) if s2's end matches
// }
var isInterleave = function(s1, s2, s3) {
    if (s1.length + s2.length !== s3.length) return false
    const cache = new Array(s1.length + 1).fill(0).map(_ => new Array(s1.length + 1).fill(false))
    for (let i = 0; i < s1.length + 1; i++) {
        for (let j = 0; j < s2.length + 1; j++) {
            if (i === 0 && j === 0) {
                cache[i][j] = true
                continue
            }
            cache[i][j] = (s1[i - 1] === s3[i + j - 1] && cache[i-1][j]) 
            || (s2[j - 1] === s3[i + j - 1] && cache[i][j - 1])
        }
    }
        
    return cache[s1.length][s2.length]
};

```
