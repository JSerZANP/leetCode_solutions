a video explaining this: https://youtu.be/_1QNutln2G4


```js
/**
 * @param {number} rowIndex
 * @return {number[]}
 */
var getRow = function(rowIndex) {
    if (rowIndex === 0) {
        return [1]
    }
    
    const prevRow = getRow(rowIndex - 1)
    const result = [1]
    prevRow.reduce((prev, item) => {
        if (prev !== 0) {
            result.push(prev + item) 
        }
        return item
    }, 0)
    result.push(1)
    return result
};
```
