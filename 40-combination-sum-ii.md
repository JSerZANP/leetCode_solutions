Video explaining this: https://youtu.be/0gY2ji6K66c


```js
// Time: worst O(2^n)
// Space: worst O(2^N)???
var combinationSum2 = function(candidates, target) {
    // sort the numbers to avoid unecessary calculations
    candidates.sort((a, b) => a - b)
    
    const result = []
    // Back Tracking
    // sum -> current sum of temp result
    // index -> starting point, avoid duplicate checks
    // tmp -> temporary result
    const walk = (sum, index, temp) => {
      // check if it satisify the condition
	  // if bigger ,the terminate the process
      if (sum >= target) {
        if (sum === target) {
          result.push(temp)
        }
        return true
      }
      
      // if not, we could add more numbers in it
      // 1 1 1 1 1 1 => 3
      for (let i = index; i < candidates.length; i++) {
        const num = candidates[i]
        // avoid duplicate results
        if (i > index && num === candidates[i-1]) continue
        const shouldTerminate = walk(sum + num, i + 1, temp.concat(num))
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
