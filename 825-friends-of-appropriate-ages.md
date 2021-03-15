Here is my video explaining it: https://youtu.be/Gknueubokx4

```js
/**
 * @param {number[]} ages
 * @return {number}
 */

// brute force 
// TLE
// var numFriendRequests = function(ages) {
//     // O(N(n - 1))
  
//     const shouldRequst = (from, to) => {
//       if (to <= 0.5 * from + 7) return false
//       if (to > from) return false
//       return true
//     }
    
//     let count = 0
//     for (let i = 0; i < ages.length; i++) {
//       for (let j = 0; j < ages.length; j++) {
//         if (i === j) continue
//         if (shouldRequst(ages[i], ages[j])) {
//           count += 1
//         }
//       }
//     }
  
//    return count
// };

// sort first
//  O(N(n - 1)/2) => O(n^2)
// var numFriendRequests = function(ages) {
//     ages.sort((a, b) => b - a)
  
//     // N - 1 + n - 2 + .. + 1
//     // N(N - 1) / 2
//     const shouldRequst = (from, to) => {
//       if (to <= 0.5 * from + 7) return false
//       if (to > from) return false
//       return true
//     }
    
//     let count = 0
//     for (let i = 0; i < ages.length - 1; i++) {
//       for (let j = i + 1; j < ages.length; j++) {
//         if (shouldRequst(ages[i], ages[j])) {
//           count += ages[i] === ages[j] ? 2 : 1
//         }
//       }
//     }
  
//    return count
// };

// Time: O(n)
var numFriendRequests = function(ages) {
    // for 16       >15 <= 16 => 
    // for each age, the range i limited
    // age is finite, so we could just do the counting for the range of each age
    
    // 1  => [8, 1] => 0
    // 2 => [9, 2] => 0
    // 0.5 * x + 7 < x => x > 14
    // 14 => [15, 14] => 0
    // 15 => [15, 15] => 1
    // 16 => [16, 16]
    // 120 => [68, 120]  
  
    // O(n) => count the range 
    
    // 1. count the ages
    const ageCount = new Array(121).fill(0)
    for (let age of ages) {
      ageCount[age] += 1
    }
    
    let result = 0
    // 2. loop through each age, and then count the range
    for (let i = 15; i < 121; i++) {
      let appropriateAgeCount = -1
      for (let j = Math.floor(0.5 * i + 7) + 1; j <= i; j++) {
        appropriateAgeCount += ageCount[j]
      }
      
      result += appropriateAgeCount * ageCount[i]
    }
  
    return result
}




```
