Here is me explaining it: https://youtu.be/ySrinuKlHP4

```js
/**
 * @param {number[]} nums
 */
// O(n) and O(n)
var Solution = function(nums) {
    // Space O(n)
    // Map<num, [index1, index]>
    const indexMap = new Map()
    
    for (let i = 0; i < nums.length; i++) {
      if (!indexMap.has(nums[i])) {
        indexMap.set(nums[i], [])
      }
      
      indexMap.get(nums[i]).push(i)
    }
  
    this.indexMap = indexMap
};

/** 
 * @param {number} target
 * @return {number}
 */
// O(1)
Solution.prototype.pick = function(target) {
    const indices = this.indexMap.get(target)
    const randomI = Math.floor(indices.length * Math.random())
    return indices[randomI]
};

/** 
 * Your Solution object will be instantiated and called as such:
 * var obj = new Solution(nums)
 * var param_1 = obj.pick(target)
 */
 ```
