Here is my youtube video: https://youtu.be/roRCxBmstHQ

```js
/**
 * @param {string} s
 * @return {boolean}
 */
var canPermutePalindrome = function(s) {
    //  aba   abba
    //  1 odd count, all even else 
    // all even
  
    // count the character, odd count must be <= 1
  
    const count = new Map()
    
    for (let char of s) {
      if (count.has(char)) {
        count.set(char, count.get(char) + 1)
      } else {
        count.set(char, 1)
      }
    }
  
    let countOfOddOccurance = 0
    for (let occurance of count.values()) {
      if (occurance % 2 === 1) {
        countOfOddOccurance += 1
      }
      
      if (countOfOddOccurance > 1) {
        return false
      }
    }
  
    return true
};
```
