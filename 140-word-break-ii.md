Here is me explaining this on youtube: https://youtu.be/sa3MVdy42MU

```js
/**
 * @param {string} s
 * @param {string[]} wordDict
 * @return {string[]}
 */

// Time: 
// T(i) = T(i - 1) + T(i - 2) + ....T(1)
//      = 2T(i - 1)
//      = O(2^n)
// Space

// S(i) = S(i - 1) + s(i - 2) + .. S(1)
//        = 2 ^ 1(s( i - 2) + s(i - 3) ... S(1))
//        = 2 ^ 2(s( i - 3) + ....S(1))
//        = 2 ^ (i - 2) (S(1))
//        = O(2 ^ n)
// 0
//      1
//          2
//            3
//      2
//      3
// aaaaaaaaaaab
// a aa aaa aaaaaa  
var wordBreak = function(s, wordDict) {
    const cache = new Map()
    // return string[]
    const walk = (i) => {
      if (cache.has(i)) return cache.get(i)
      if (i >= s.length) return []
      
      const matches = []
      // search for words to match
      for (let word of wordDict) {
        const length = word.length
        const nextIndex = i + length
        if (s.slice(i, i + length) === word) {
          if (nextIndex >= s.length) {
            matches.push(word)
          } else {
            const nextMatches = walk(i + length)
            for (let sentence of nextMatches) {
              matches.push(word + ' ' + sentence)
            }
          }
        }
      }
      cache.set(i, matches)
      return matches
    }
    
    return walk(0)
};
```
