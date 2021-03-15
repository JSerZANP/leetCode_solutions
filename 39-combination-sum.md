An explaining video: https://youtu.be/zagXJO34FMQ


```js
/**
 * @param {number[]} candidates
 * @param {number} target
 * @return {number[][]}
 */
var combinationSum = function(candidates, target) {
    // Brute Force => 2^n

    candidates.sort((a, b) => a - b)
    
    const result = []
    // Back Tracking
    const walk = (sum, index, temp) => {
      // check if it satisify the condition
      if (sum >= target) {
        if (sum === target) {
          result.push(temp)
        }
        return true
      }
    
      
      // if not, we could add more numbers in it
      for (let i = index; i < candidates.length; i++) {
        const num = candidates[i]
        
        const shouldTerminate = walk(sum + num, i, temp.concat(num))
        if (shouldTerminate) {
          break
        }
      }
      
      return false
    }
    
    walk(0,0,[])
  
    return result
};
```
