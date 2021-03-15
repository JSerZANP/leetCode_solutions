Me explaining it on youtube https://youtu.be/2-zkNDQGjKY

```js
/**
 * @param {string} s
 * @return {boolean}
 */

// Time: O(n)
// Space: O(1)
// var isNumber = function(s) {
//    s = s.trim()
  
//    // 0 ~ 9 . + - e
//    // 0 ~ 9 basically everywher  002
//    // +- => at index 0, or right after e
//    // . => max 1, must not be after e
//    // e => max 1, must have numers before & after
  
  
//    // loop throught each character
//    // check if rules are broken
  
//    let hasDigits = false
//    let isDigitMissingAfterE = false
//    let hasDot = false
//    let hasE = false
   
//    for (let i = 0; i < s.length; i++) {
//      switch (s[i]) {
//        case '0':
//        case '1':
//        case '2':
//        case '3':
//        case '4':
//        case '5':
//        case '6':
//        case '7':
//        case '8':
//        case '9':
//          hasDigits = true
//          isDigitMissingAfterE = false
//          break
//        case '+':
//        case '-':
//          if (i !== 0 && s[i - 1] !== 'e') {
//            return false
//          }
//          break
//        case '.':
//          if (hasDot || hasE) return false
//           hasDot = true
//           break
//        case 'e':
//          if (hasE || !hasDigits ) return false
//          hasE = true
//          isDigitMissingAfterE = true
//          break
//        default:
//           return false
//      }
//    }
  
//    return hasDigits && !isDigitMissingAfterE
// };

var isNumber = function(s) {
   s = s.trim()
  
   // 0 ~ 9 . + - e
   // 0 ~ 9 basically everywher  002
   // +- => at index 0, or right after e
   // . => max 1, must not be after e
   // e => max 1, must have numers before & after
  
  
   // loop throught each character
   // check if rules are broken
  
   let hasDigits = false
   let isDigitMissingAfterE = false
   let hasDot = false
   let hasE = false
   
   for (let i = 0; i < s.length; i++) {
     const char = s[i]
     if (char >= '0' && char <= '9') {
         hasDigits = true
         isDigitMissingAfterE = false
     } else if (char === '+' || char === '-') {
         if (i !== 0 && s[i - 1] !== 'e') {
           return false
         }
     } else if (char === '.') {
         if (hasDot || hasE) return false
          hasDot = true
     } else if (char === 'e') {
         if (hasE || !hasDigits ) return false
         hasE = true
         isDigitMissingAfterE = true
     } else {
       return false
     }
   }
  
   return hasDigits && !isDigitMissingAfterE
};
```
