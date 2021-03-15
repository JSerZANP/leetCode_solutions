My video for this problem: https://youtu.be/VxvztgVvICM


```js
/**
 * @param {string} s1
 * @param {string} s2
 * @return {boolean}
 */

// great     rgeat
// one root of the binary tree
// g  reat    g will be at the beginning or the end

// possible recursion solution

// T(N) = 2 * (T(1) + T(N - 1) + T(2) + T(N - 2) ......T(N - 1) + T(1))
//      = 2 ^ 2 * (T(N-1) + T(N - 2) + ... + T(1)
//        = 2 ^ 2 * (2 ^ 2 * (T(N - 2) + ...T())  )
//        = 4 * (4 + 1) * (T(N-2) + ...T)
//        = 2 ^ N
// var isScramble = function(s1, s2) {
//     // possible root position
//     // s1.length - 1
    
//     if (s1.length !== s2.length) {
//         return false
//     }
    
//     if (s1.length === 1) {
//         return s1 === s2
//     }
    
//     //O(n)
//     for (let i = 0; i < s1.length - 1; i++) {
//        const left = s1.slice(0, i + 1) 
//        const right = s1.slice(i + 1)
       
//        const left2_1 = s2.slice(0, i + 1)
//        const right2_1 = s2.slice(i + 1)
       
//        const left2_2 = s2.slice(s2.length - 1 - i)
//        const right2_2 = s2.slice(0, s2.length - 1 - i)
       
//        if ( (isScramble(left, left2_1) && isScramble(right, right2_1)) || 
//            (isScramble(left, left2_2) && isScramble(right, right2_2))) {
//            return true
//        }
//     }
    
//     return false
// };


// in recursion, passing down substring, wich is s1.slice(i, j)
// each comparsion [i, j, k, l ] => [i, j, length], 1 <= length <= n
// memoization 
var isScramble = function(s1, s2) {
    if (s1.length !== s2.length) {
        return false
    }
    
    const n = s1.length
   
    const cache = Array(n).fill(0).map(_ => {
        return Array(n).fill(0).map(_ => {
            return Array(n).fill(false)
        })
    })

    
    for (let l = 1; l <= n; l++) {
        for (let i = 0; i < n - l + 1; i++) {
            for (let j = 0; j < n - l + 1; j++) {
                if (l === 1) {
                    cache[i][j][l] = s1[i] === s2[j]
                } else {
                    let result = false
                    for (let k = 1; k < l; k++) {
                        // gre  at     rge  at
                       if ((cache[i][j][k] && cache[i + k ][j + k][l - k])
                           || (cache[i][j + l - 1 - k + 1][k] && cache[i + k][j][l - k])) {
                           result = true
                           break
                       }
                    }
                    cache[i][j][l] = result
                }
            }
            
        }
    }
    return cache[0][0][n]
};



```
