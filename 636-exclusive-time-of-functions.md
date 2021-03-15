Here is a video explaining it: https://youtu.be/pO3EQ5y4V34
```js
/**
 * @param {number} n
 * @param {string[]} logs
 * @return {number[]}
 */

// Time: O(count of logs)
// Space: worst O(n)
var exclusiveTime = function(n, logs) {
    // use a stack to keep track of the top most function
    // upate the time of each function by segement
  
    const callStack = []  // Array<string>
    
    const result = new Array(n).fill(0)
    
    let prevTimestamp = 0
    for (let log of logs) {
      const [functionId, flag, _timestamp] = log.split(':')
      const timestamp = parseInt(_timestamp, 10)
      
      if (callStack.length === 0) {
        callStack.push(functionId) // better confirm with interviewer
      } else {
        if (flag === 'end') {
          const length = timestamp - prevTimestamp + 1
          const currentFunction = callStack.pop()
          result[currentFunction] += length
          prevTimestamp = timestamp + 1
        } else {
          const length = timestamp - prevTimestamp
          result[callStack[callStack.length - 1]] += length
          callStack.push(functionId)
          prevTimestamp = timestamp
        }
      }
    }
  
    return result
};
```
