A video explaining this: https://youtu.be/CuMW2upRBc8


```js
/**
 * @param {string} s
 * @param {string} t
 * @return {string}
 */
// var minWindow = function(s, t) {
//     // ADOBECODEBANC  ABCB
//     // ADOBECODEBANC
    
//     // target A1B2C
    
//     // count, check against target
//     // missing set [A, B, C]
  
//     // A          [ B, C]
//     // .  B       [ B, C]
//     // .    C     [ B]
//     // .        B []  => possible solution
  
//     let result = ''
//     if (s === '' || t === '') return result
  
//     // count the target string
//     const target = new Map()
//     const count = new Map()
//     const missingChars = new Set()
//     const indices = []
    
//     for (let i = 0; i < t.length; i++) {
//       if (!target.has(t[i])) {
//         target.set(t[i], 1)
//       } else {
//         target.set(t[i], target.get(t[i]) + 1)
//       }
      
//       count.set(t[i], 0)
//       missingChars.add(t[i])
//     }
//     // console.log(target, count, missingChars)
//     for (let i = 0; i < s.length; i++) {
//       const char = s[i]
      
//       // update the count
//       if (target.has(char)) {
//         count.set(char, count.get(char) + 1)
//         // if occurence is enough
//         if (count.get(char) >= target.get(char)) {
//           missingChars.delete(char)
//         }
        
//         indices.push([char, i])
//       }
//       // console.log('checking', s.slice(0, i + 1), (missingChars.size))
//       // if it is possible result
//       // BCBCA => CBCA
//       // while loop to check over and over agian
//       while (missingChars.size === 0) {
//         const possibleResult = s.slice(indices[0][1], indices[indices.length - 1][1] + 1)
//         if (result === '' || possibleResult.length < result.length) {
//           result = possibleResult
//         }
        
//         // remove the first index
//         const firstIndex = indices[0]
//         indices.shift()
//         // update the count
//         count.set(firstIndex[0], count.get(firstIndex[0]) - 1)
//         // update the missing 
//         if (count.get(firstIndex[0]) < target.get(firstIndex[0])) {
//           missingChars.add(firstIndex[0])
//         }
//       }
//     }
  
//     return result
// };



var minWindow = function(s, t) {

  // keep start, end, then move end along s
  
  // count occurence of the target, when found no missing character, it is possible min substring
  // move start to the right, update counting, until missing character is found
  
  const missingChars = new Set()
  const targetCountMap = new Map()
  
  for (let char of t) {
    missingChars.add(char)
    if (targetCountMap.has(char)) {
      targetCountMap.set(char, targetCountMap.get(char) + 1)
    } else {
      targetCountMap.set(char, 1)
    }
  }
  
  let result = ''
 

  const countMap = new Map()
  
  const addCount = (char) => {
    if (countMap.has(char)) {
      countMap.set(char, countMap.get(char) + 1)
    } else {
      countMap.set(char, 1)
    }
    
    if (countMap.get(char) === targetCountMap.get(char)) {
      missingChars.delete(char)
    }
  }
  
  const removeChar = (char) => {
    countMap.set(char, countMap.get(char) - 1)
    if (countMap.get(char) < targetCountMap.get(char)) {
      missingChars.add(char)
    }
  }
  
  const getNextTargetChar = (i) => {
    while (i < s.length && !targetCountMap.has(s[i])) {
      i += 1
    }
    
    return i
  }
  
  
  let start = getNextTargetChar(0)
  let end = start
  
  while (end < s.length) {
  
    const char = s[end]
    
    if (targetCountMap.has(char)) {
      addCount(char)
      

      while (missingChars.size === 0) {
        // possible sub string
        const subStr = s.slice(start, end + 1)
        if (result === '' || result.length > subStr.length) {
          result = subStr
        }
      
        const head = s[start]
        if (targetCountMap.has(head)) {
          removeChar(head)
        }

        start = getNextTargetChar(start + 1)
      }
    }
    
    end = getNextTargetChar(end + 1)
  }
  
  
  return result
}
```
