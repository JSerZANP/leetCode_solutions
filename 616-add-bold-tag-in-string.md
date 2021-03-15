Here is me explaining it on youtube: https://youtu.be/tLOvSNpYtso


```js
/**
 * @param {string} s
 * @param {string[]} dict
 * @return {string}
 */
var addBoldTag = function(s, dict) {
    // loop through s
    // find the longest bold word end index for each index
    // connect them if needed
    // collect the result
  
    // return -1 if no bold
    // return the last bold index if found
    
    const getBoldEnd = (i) => {
      let end = i
      let start = i
      
      let shouldBeBold = false
      
      while (start <= end) {
        for (let word of dict) {
          // if found a word, extend the end
          if (word === s.slice(start, start + word.length)) {
            shouldBeBold = true
            end = Math.max(end, start + word.length - 1)
          }
        }
        
        start += 1
      }
      
      if (shouldBeBold) return end
      return -1
    }
    
    let result = ''
    
    for (let i = 0; i < s.length; i++) {
      let boldEnd = getBoldEnd(i)
      // it is bold, check if connected bold word exits
      while (boldEnd !== -1) {
        const next = getBoldEnd(boldEnd + 1)
        
        if (next === -1) {
          break
        }
        
        boldEnd = next
      }
      
      if (boldEnd !== -1) {
        result += '<b>' + s.slice(i, boldEnd + 1) + '</b>'
        i = boldEnd
      } else {
        result += s[i]
      }
      
    }
  
    return result
    
};
```
