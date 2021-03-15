Youtube video explaining this: https://youtu.be/KiOkoeZROLo


```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var permuteUnique = function(nums) {
    const result = []
    
    nums.sort((a, b) => a - b)
    
    const walk = (temp, rest) => {
      if (rest.length === 0) {
        result.push(temp)
        return
      }
      
      for (let i = 0; i < rest.length; i++) {
        if (rest[i] === rest[i - 1]) continue
        const newRest = rest.slice(0)
        newRest.splice(i, 1)
        walk(temp.concat(rest[i]), newRest)
      }
    }
    
    walk([], nums)
  
    return result
};
```
