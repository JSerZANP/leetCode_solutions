A video explaining: https://youtu.be/ntE-tgQC988

```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {boolean}
 */
var canArrange = function(arr, k) {
    // 1,2,3,4,5,10,6,7,8,9, -1
  
    //  2 3 4 0 0 1 2  , 4
    // 
  
    // ( a + b ) % k === 0
    // (a % k + b % k) % k === 0
    // 
  
    // about the count of each number's modulelo?
    // find the pair by direct access map
    // if no single element left, then OK
  
    // Map<modulelo, count>
  
    const countMap = new Map()
    for (let num of arr) {
      
      const mod = num > 0 ? num % k : (k - (-num) % k) % k
      if (countMap.has(mod)) {
        countMap.set(mod, countMap.get(mod) + 1)
      } else {
        countMap.set(mod, 1)
      }
    }
    // remove the pairs
    // -1,1,-2,2,-3,3,-4,4
    // 2 1 1 2 0 0 
    for (let [mod, count] of countMap) {
      if (mod === 0) {
        if (count % 2 !== 0) {
          return false
        }
         countMap.delete(mod)
      } else {
        const counterpart = k - mod

        if (countMap.get(counterpart) !== count) {
          // not match
          return false
        }
        countMap.delete(mod)
        countMap.delete(counterpart)
      }
    }
  
    return true
};
```
