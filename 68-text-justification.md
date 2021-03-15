Here is a video explaining: https://youtu.be/xoeMhTvg11M

```js
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
var fullJustify = function(words, maxWidth) {
    const result = []
    let chunk = []
    let chunkLength = 0
    
    const generateSpaces = (n) => {
      if (n === 0) return ''
      return Array(n).fill(' ').join('')
    }
    
    const flush = (isLast) => {
      // transform chunk into a string
      let spaces = Array(chunk.length).fill('')
      if (isLast) {
        for (let i = 0; i < spaces.length; i++) {
          if (i < spaces.length - 1) {
            spaces[i] = ' '
          } else {
            const rest = maxWidth - chunkLength - i
            spaces[i] = generateSpaces(rest)
          }
        }
      } else {
        // last space should be empty
        if (spaces.length === 1) {
          spaces[0] = generateSpaces(maxWidth - chunkLength)
        } else {
          const base = Math.floor((maxWidth - chunkLength) / (spaces.length - 1))
          const rest = maxWidth - chunkLength - base * (spaces.length - 1)
          for (let i = 0; i < spaces.length - 1; i++) {
            if (i < rest) {
              spaces[i] = generateSpaces(base + 1)
            } else {
              spaces[i] = generateSpaces(base)
            }
          }
        }
      }
      
      // genrate the string
      result.push(chunk.map((word, i) => word + spaces[i]).join(''))
      
      chunk = []
      chunkLength = 0
    }
    
    for (let i = 0; i < words.length + 1; i++) {
      const word = words[i]
      // whether word could be put into the chunk
      if (i === words.length) {
        flush(true /* last chunk */)
      } else if (chunkLength + word.length + chunk.length <= maxWidth) {
        chunk.push(word)
        chunkLength += word.length
      } else {
        flush()
        i -= 1
      }
    }
  
    return result
    
};
```
