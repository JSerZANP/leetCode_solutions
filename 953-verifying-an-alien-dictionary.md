me explaining on youtube: https://youtu.be/jULIeSn0RuY

```js
/**
 * @param {string[]} words
 * @param {string} order
 * @return {boolean}
 */

// Time: O(n * m)
// var isAlienSorted = function(words, order) {
    
//     const dict = new Map()
    
//     for (let i = 0; i < order.length; i++) {
//         dict.set(order[i], i)
//     }
    
//     const compareChar = (a, b) => {
//         return dict.get(a) - dict.get(b)
//     }
    
//     const compareWord = (a, b) => {
//         let i = 0
//         let j = 0
//         while (i < a.length && j < b.length) {
//             const compared = compareChar(a[i], b[j])
//             if (compared > 0) {
//                 return 1
//             } else if (compared < 0) {
//                 return -1
//             }
            
//             i += 1
//             j += 1
//         }
        
//         if (i === a.length) {
//             return j === b.length  ? 0 : -1
//         } else {
//             return 1
//         }
//     }
    
//     for (let i = 1; i < words.length; i++) {
//         if (compareWord(words[i - 1], words[i]) > 0) {
//             return false
//         }
//     }
    
//     return true
// };


// Time: O(N M)
// var isAlienSorted = function(words, order) {
    
//     const dict = new Map()
//     for (let i = 0; i < order.length; i++) {
//         dict.set(order[i], i + 1)
//     }
  
//     // has is based on 20 digits , 26 based number, in string
//     const hash = (str) => {
//         const segs = []
//         for (let i = 0; i < str.length; i++) {
//             const index = dict.get(str[i])
//             segs.push(index < 10 ? '0' + index : index)
//         }
//         return segs.join('')
//     }
    
//     let prevHashed = ''
//     for (let i = 0; i < words.length; i++) {
//         const hashed = hash(words[i])
//         console.log(hashed)
//         if (hashed < prevHashed) {
//             return false
//         }
//         prevHashed = hashed
//     }
    
//     return true
// };

// var isAlienSorted = function(words, order) {
    
//     const realOrder = 'abcdefghijklmnopqrstuvwxyz'
//     const dict = new Map()
//     for (let i = 0; i < order.length; i++) {
//         dict.set(order[i], i)
//     }
  
//     // has is based on 20 digits , 26 based number, in string
//     const translate = (str) => {
//         const segs = []
//         for (let i = 0; i < str.length; i++) {
//             const index = dict.get(str[i])
//             segs.push(realOrder[index])
//         }
//         return segs.join('')
//     }
    
//     let prev = ''
//     for (let i = 0; i < words.length; i++) {
//         const tranlsated = translate(words[i])
//         if (tranlsated < prev) {
//             return false
//         }
//         prev = tranlsated
//     }
    
//     return true
// };

var isAlienSorted = function(words, order) {
  
  // Map<char, index>
  const indexMap = new Map()
  
  for (let i = 0; i < order.length; i++) {
    indexMap.set(order[i], i)
  }
  
  const compare = (char1, char2) => {
    if (char1 === char2) return 0
    if (indexMap.get(char1) < indexMap.get(char2)) {
      return -1
    } else {
      return 1
    }
  }
  
  const isWordBefore = (word1, word2) => {
    for (let i = 0; i < word1.length; i++) {
      if (word2[i] === undefined) {
        return false
      }
      
      const compared = compare(word1[i], word2[i])
      if (compared === -1) return true
      if (compared === 1) return false
    }
    
    return true
  }
  
  
  for (let i = 0; i < words.length - 1; i++) {
    if (!isWordBefore(words[i], words[i + 1])) {
      return false
    }
  }
  return true
}
```
