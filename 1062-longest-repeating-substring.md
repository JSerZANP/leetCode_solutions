Me explaining this on youtube: https://youtu.be/vXqYXuikef4

```js
/**
 * @param {string} S
 * @return {number}
 */

// brute force 
// loop through start index pair(n ^ 2)
// foreach pair, check the longest length (n)

// Space: O(1)
// var longestRepeatingSubstring = function(S) {
//     let max = 0
    
//     for (let i = 0 ; i < S.length - 1; i++) {
//         for (let j = i + 1; j < S.length; j++) {
//             let k = 0
//             while (S[i + k] === S[j + k]) {
//                 k += 1
//                 max = Math.max(k, max)
//             }
//         }
//     }
    
//     return max
// };


// aabcaabdaab
// a - a 

// dynamic programming
// f(i, j) longest matched string, ending at i, j
// f(i, j) = f(i - 1, j - 1) + 1, if S[i] === S[j]
// 0  if not

// Time: O(n ^ 2)
// Space: O(n ^ 2)
// var longestRepeatingSubstring = function(S) {
//    // cache the result
//     const results = Array(S.length).fill(0).map(_ => Array(S.length))
    
//     let max = 0
//     for (let i = 0; i < S.length - 1; i++) {
//         for (let j = i + 1; j < S.length; j++) {
//             let count = 0
//             if (i === 0) {
//                 count = S[i] === S[j] ? 1 : 0
//             } else {
//                 count = S[i] === S[j] ? results[i - 1][j - 1] + 1 : 0
//             }
//             max = Math.max(max, count)
//             results[i][j] = count
//         }
//     }
    
//     return max
// };


// aabcaabdaab
// a a
// aa ab
// aa bc
// ...
// aa aa
// aab aab

// basic idea,
// find the first mach of length i
// find the next match of length i + 1, starting right from previous position

// abcde, aaaaa
// Time: worst is that all chars are different, O(n ^ 2)
// Space: O(1)
var longestRepeatingSubstring = function(S) {
   let max = 0
   
   for (let i = 0; i < S.length - max - 1; i++) {
       let nextTarget = S.slice(i, i + max + 1)
       for (let j = i + 1; j < S.length - max; j++) {
           const substr = S.slice(j, j + max + 1)
           if (substr === nextTarget) {
               nextTarget += S[i + max + 1]
               max += 1
               j -= 1
           }
       }
   }
    
   return max
};









```
