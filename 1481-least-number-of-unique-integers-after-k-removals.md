Hear me explaining it on youtube: https://youtu.be/CNCCQ4UndDs

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number}
 */

// Time: O(NlogN)
// space: O(N)
var findLeastNumOfUniqueInts = function(arr, k) {
    // maximize the uniqueness from k element
    // by couting the numbers => sort
    
    // space: O(N)
    const count = new Map()
    
    // O(n)
    for (let num of arr) {
      if (count.has(num)) {
        count.set(num, count.get(num) + 1)
      } else {
        count.set(num, 1)
      }
    }
  
    const uniqueCounts = [...count.values()]
    
    // O(NlogN)
    uniqueCounts.sort((a, b) => a - b)
    
    let removedCount = 0
    let removedUniqueCount = 0
    // O(N)
    for (let count of uniqueCounts) {
      removedCount += count
      if (removedCount <= k) {
        removedUniqueCount += 1
      } else {
        break
      }
    }
  
    return uniqueCounts.length - removedUniqueCount;
};
```
