Here is my video explaing: https://youtu.be/ClXso8GXiXs

```js
/**
 * @param {character[]} chars
 * @return {number}
 */
var compress = function(chars) {
    // "a","a","b","b","c","c","c"
    
    // there are 3 c
    // "a", "2", "b", "2", "c", "3"
    
    
    // 1. current letter
    // 2. current letter count
    // 3. index to put letter/number
    
    let currentLetter = null
    let currentLetterCount = 0
    let indexToPut = 0
    
    for (let i = 0; i < chars.length + 1; i++) {
        const char = chars[i]
        
        if (char !== currentLetter) {
            
            if (currentLetter !== null) {
                chars[indexToPut] = currentLetter
                indexToPut += 1
                if (currentLetterCount > 1) {
                    const countInStr = `${currentLetterCount}`
                    for (let digit of countInStr) {
                        chars[indexToPut] = digit
                        indexToPut += 1
                    }
                }
            }
            
            currentLetter = char
            currentLetterCount = 1
        } else {
            currentLetterCount += 1           
        }
    }
    
    return indexToPut
};
```
