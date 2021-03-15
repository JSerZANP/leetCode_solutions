Here is my youtube video explaining it: https://youtu.be/T84Nvyubl-c

```js
/**
 * @param {string} S
 * @return {string}
 */

function* nextWord(str) {
  let start = 0
  let i = 0
  while (i < str.length + 1) {
    if (str[i] === ' ' || i === str.length) {
      yield str.slice(start, i)
      start = i + 1
    }
    i += 1
  }
}

const VOWELS = new Set(['a', 'e', 'i', 'o', 'u'])

// Time: O(n)
// space: O(1)
var toGoatLatin = function(S) {
    const wordGen = nextWord(S)
    
    let result = ''
    
    let appendix = 'a'
    
    for (let word of wordGen) {
      let transformed = null
      if (VOWELS.has(word[0].toLowerCase())) {
        transformed = word + 'ma'
      } else {
        transformed = word.slice(1) + word[0] + 'ma'
      }
      
      transformed += appendix
      appendix += 'a'
      
      result += result === '' ? transformed : (' ' + transformed)
    }
  
    return result
};
```
