Here is my youtube video link explaining this: https://youtu.be/AEYOwT_-p8o


```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function(nums1, nums2) {
    //  nums1 = [1,2,2,1], nums2 = [2,2]
  
    // n  m
    // O(nm) + space O(min(n, m))
  
    // preprocess nums2 to a Map<number, count>
    // O(n + m) + space(min(n, m))
    // process the shorter one
  
    let preprocessTarget = nums1
    let loopTarget = nums2
    
    if (nums1.length > nums2.length) {
      preprocessTarget = nums2
      loopTarget = nums1
    }
  
    // Map<element, number>
    const countMap = new Map()
    for (let num of preprocessTarget) {
      if (countMap.has(num)) {
        countMap.set(num, countMap.get(num) + 1)
      } else {
        countMap.set(num, 1)
      }
    }
    
  
    const result = []
    
    for (let num of loopTarget) {
      if (countMap.has(num)) {
        result.push(num)
        
        const count = countMap.get(num)
        if (count === 1) {
          countMap.delete(num)
        } else {
          countMap.set(num, count - 1)
        }
      }
    }
  
    return result
};
  
  
  
  
  
  
  
  
  
  
  
  
  ```
