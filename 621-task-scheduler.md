me explaining it on youtube: https://youtu.be/RrnDKOh2jbM


```js
/**
 * @param {character[]} tasks
 * @param {number} n
 * @return {number}
 */
var leastInterval = function(tasks, n) {
    // "A","A","A","B","B","B"
    // A B 0 A B 0 A B
  
    // A A A A  B B
    // A (B C D E 0 0 ) A ( B C D E 0 0 ) A (B C E 0 0 ) A (B)
  
    // count of each task
    const countOfTask = new Array(26).fill(0)
    
    let maxCount = 0
    const codeForA = 'A'.charCodeAt(0)
    
    for (let task of tasks) {
      const index = task.charCodeAt(0) - codeForA
      countOfTask[index] += 1
      if (countOfTask[index] > maxCount) {
        maxCount = countOfTask[index]
      }
    }
  
    // determine how many tasks are to the maxCount
    let taskCountOfMaxCount = 0
    for (let count of countOfTask) {
      if (count === maxCount) {
        taskCountOfMaxCount += 1
      }
    }
    
    const intervalsRequred = (maxCount - 1) * (n + 1) + taskCountOfMaxCount
    return Math.max(intervalsRequred, tasks.length)
};
```
