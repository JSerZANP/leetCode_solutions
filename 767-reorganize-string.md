me explaining it on youtube: https://youtu.be/xydV-tkF3Fk

```js
/**
 * @param {string} S
 * @return {string}
 */

// baaba  => babaa => baaba => ababa

// Time: 2 * O(n^2) => O(n ^ 2)
// Space: O(n)
// var reorganizeString = function(S) {
//     const chars = S.split('')
    
//     const swap = (i, j) => {
//       const temp = chars[i]
//       chars[i] = chars[j]
//       chars[j] = temp
//     }
    
//     let isReorganizable = true
//     // swap when found adjacent same letters
//     for (let i = 1; i < chars.length; i++) {
//       if (chars[i - 1] === chars[i]) {
//         let isSwapped = false
//         for (let k = i + 1; k < chars.length; k++) {
//           if (chars[k] !== chars[i]) {
//             swap(k, i)
//             isSwapped = true
//             break
//           }
//         }
        
//         if (!isSwapped) {
//           isReorganizable = false
//           break
//         }
//       }
//     }
  
//     if (isReorganizable) {
//       return chars.join('')
//     }
  
//     isReorganizable = true
//     // swap when found adjacent same letters
//     for (let i = chars.length - 2; i > -1; i--) {
//       if (chars[i] === chars[i + 1]) {
//         let isSwapped = false
//         for (let k = i - 1; k > -1; k--) {
//           if (chars[k] !== chars[i]) {
//             swap(k, i)
//             isSwapped = true
//             break
//           }
//         }
        
//         if (!isSwapped) {
//           isReorganizable = false
//           break
//         }
//       }
//     }
  
//    if (isReorganizable) {
//       return chars.join('')
//     } else {
//       return ''
//     }
    
// };



// "baaba"  => " a b c a b c a b"
// aaabc => abaca

// Time: O(n)
// Space: O(26) + O(n) => O(n)
var reorganizeString = function(S) {
  
    // count each letter
    const counts = new Array(26).fill(0)
    
    const codeForA = 'a'.charCodeAt(0)
    for (let i = 0; i < S.length; i++) {
      counts[S.charCodeAt(i) - codeForA] += 1
    }
  
    // get the most letter
    let mostLetterCode = undefined
    let mostCount = 0
    for(let i = 0; i < counts.length; i++) {
      if (counts[i] > mostCount) {
        mostCount = counts[i]
        mostLetterCode = i + codeForA
      }
    }
  
    if (S.length - mostCount < mostCount - 1) {
      return ''
    }
  
    // collect the result
    const result = Array(S.length)    
    let currentPosition = 0
    
    // first put the mostLetter
    const mostLetter = String.fromCharCode(mostLetterCode)
    for (let i = 0; i < mostCount; i++) {
      result[currentPosition] = mostLetter
      currentPosition += 2
    }
    
    // put the rest letter accordingly
    for (let i = 0; i < counts.length; i++) {
      if (counts[i] === 0 || i + codeForA === mostLetterCode) continue
      const letter = String.fromCharCode(codeForA + i)
      let j = counts[i]
      while (j > 0) {
        if (currentPosition > S.length - 1) currentPosition = 1
        result[currentPosition] = letter
        currentPosition += 2
        j -= 1
      }
    }
    
    return result.join('')
};






```
