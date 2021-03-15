Youtube video explaining this: https://youtu.be/kONcHqWCmBo
```js
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
// Time: n!
var permute = function(nums) {
    const result = []
    
    const walk = (temp, rest) => {
      if (rest.length === 0) {
        result.push(temp)
        return
      }
      
      for (let i = 0; i < rest.length; i++) {
        const newRest = rest.slice(0)
        newRest.splice(i, 1)
        walk(temp.concat(rest[i]), newRest)
      }
    }
    
    walk([], nums)
  
    return result
};
```
