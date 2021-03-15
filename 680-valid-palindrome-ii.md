Me explaining this on youtube: 
https://youtu.be/dqueHLhsUyI

```js
/**
 * @param {string} s
 * @return {boolean}
 */

// O(n)
var validPalindrome = function(s) {

    const check = (start, end, maxRemovals) => {
      if (start >= end) return true
      if (s[start] === s[end]) {
        return check(start + 1, end - 1,maxRemovals)
      }
      
      if (maxRemovals > 0) {
        if (check(start + 1, end, maxRemovals - 1)) return true
        return check(start, end - 1, maxRemovals - 1)
      }
      
      return false
    }
    
    return check(0, s.length - 1, 1)
};


// Time O(n)
// Space O(1)
// var validPalindrome = function(s) {
//     // choos the center, expand two ways to compare
//     // removal of  a charater could only be on the left or on the right
//     // O(3n)
    
//     // removal: 0, -1 (left). 1 (right)
//     const check  = (startLeft, startRight, removal) => {
//       while (startLeft > -1) {
//         if (s[startLeft] !== s[startRight]) {
//           if (removal === 0) return false
//           if (removal < 0) {
//             removal += 1
//             startRight -= 1
//           } else {
//             removal -= 1
//             startLeft += 1
//           }
//         }

//         startLeft -= 1
//         startRight += 1
//       }
//       return true
//     }
    
//     let startLeft
//     let startRight
//     if (s.length % 2 === 0) {
//       startLeft = s.length / 2 - 1
//       startRight = s.length / 2
//     } else {
//        startLeft = (s.length - 1) / 2
//        startRight = startLeft
//     }
  
//     if (check(startLeft, startRight, 0)) return true
    
//     // if we remove at left half
//     if (s.length % 2 === 0) {
//       startLeft = s.length / 2
//       startRight = startLeft
//     } else {
//        startLeft = (s.length - 1) / 2
//        startRight = startLeft + 1
//     }

    
//     if (check(startLeft, startRight, -1)) return true
  
  
//     // if we remove at right half
//     if (s.length % 2 === 0) {
//       startLeft = s.length / 2 - 1
//       startRight = startLeft
//     } else {
//        startLeft = (s.length - 1) / 2 - 1
//        startRight = startLeft + 1
//     }
  
    
//     if (check(startLeft, startRight, 1)) return true
  
//     return false
// };

```
