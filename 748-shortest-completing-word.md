Here is my video explaining it : https://youtu.be/pJPiwI4hot4

```js
/**
 * @param {string} licensePlate
 * @param {string[]} words
 * @return {string}
 */

// n k

// Time: O(nk)
// space: O(k)
var shortestCompletingWord = function(licensePlate, words) {
    // idea
    // pre count the licensePlate for each letter
    // loop through the words and check if satisfied
    // keep track of the shortest
  
  
    let result = null
    
    const licensePlateCount = new Map()
    
    for (let letter of licensePlate) {
      if (/[a-z]/i.test(letter)) {
        const _letter = letter.toLowerCase()
        if (licensePlateCount.has(_letter)) {
          licensePlateCount.set(_letter, licensePlateCount.get(_letter) + 1)
        } else {
          licensePlateCount.set(_letter, 1)
        }
      }
    }
  
    const satisfy = (word) => {
      const wordLetterCount = new Map()
      for (let _letter of word) {
        if (wordLetterCount.has(_letter)) {
          wordLetterCount.set(_letter, wordLetterCount.get(_letter) + 1)
        } else {
          wordLetterCount.set(_letter, 1)
        }
      }
      
      for (let [letter, count] of licensePlateCount) {
        if ((wordLetterCount.get(letter) || 0) < count) {
          return false
        }
      }
      
      return true
    }
    
    
    for (let word of words) {
      if (satisfy(word) && (result === null || result.length > word.length)) {
        result = word
      }
    }
  
    return result
};
```
