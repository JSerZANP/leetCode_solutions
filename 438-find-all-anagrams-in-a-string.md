Here is my video of explaining this: https://youtu.be/nT9TG2RuVfs

```js
/**
 * @param {string} s
 * @param {string} p
 * @return {number[]}
 */

// Time: O(sp)
// space: O(26) => O(1)
// var findAnagrams = function(s, p) {
//     // naively, compare all the possible substrings
//     // sort to decide anagram
//     // n(s * (plogp  + p)) => O(splogp)
    
//     // try to hash substrings? and then compare with O(1) => O(s)
//     // [1,1,20100,.....] '0101250002'
    
//     // counting? [1,1,20100,.....] for p => O(p)
  
//     const countForP = new Array(26).fill(0)
//     // 1. count for p
//     const codeForA = 'a'.charCodeAt(0)
//     for (let i = 0; i < p.length; i++) {
//        const index = p.charCodeAt(i) - codeForA
//        countForP[index] += 1
//     }
  
    
//     const result = []
//     for (let i = 0; i < s.length - p.length + 1; i++) {
//       const count = countForP.slice(0)
//       let k = i
//       for (; k < i + p.length; k++) {
//         const index = s.charCodeAt(k) - codeForA
//         if (count[index] === 0) {
//           break
//         } else {
//           count[index] -= 1
//         }
//       }
      
//       if (k === i + p.length) {
//         result.push(i)
//       }
//     }
  
//     return result
// };


// sliding window
var findAnagrams = function(s, p) {
    const codeForA = 'a'.charCodeAt(0)
      
    const countForP = new Array(26).fill(0)

    for (let i = 0; i < p.length; i++) {
       const index = p.charCodeAt(i) - codeForA
       countForP[index] += 1
    }
    
    const equal = (arr1, arr2) => {
      if (arr1.length !== arr2.length) return false
      for (let i = 0; i < arr1.length; i++) {
        if (arr1[i] !== arr2[i]) {
          return false
        }
      }
      return true
    }
    
    const result = []
    const countForS = new Array(26).fill(0)
    for (let i = 0; i < s.length; i++) {
      const index = s.charCodeAt(i) - codeForA
      countForS[index] += 1
      
      if (i > p.length - 1) {
        // remove the head
        const index = s.charCodeAt(i - p.length) - codeForA
        countForS[index] -= 1
      }
      
      if (i >= p.length - 1) {
        // check if counts meets 
        if (equal(countForS, countForP)) {
          result.push(i - p.length + 1)
        }
      }
    }
  
    return result
};
```
