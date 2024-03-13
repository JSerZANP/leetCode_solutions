```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number[]}
 */
// var maxSlidingWindow = function(nums, k) {
//     if (nums.length < k) return []
//     // naive solution
//     // O(n * k)
     
//     const result = []
//     for (let i = k - 1; i < nums.length; i++) {
//        let max = nums[i]
//        for (let j = i - 1; j >= i - (k - 1); j--) {
//           max = Math.max(max, nums[j])
//        }
//        result.push(max)
//     }
    
//     return result
// };


// [1]
// [3 * 2]
// [3 * 2, -1] 3
// [3 * 1, -1, -3] 3
// [5 * 3] 5
// [5 * 2, 3] 5
// [6 * 3] 6
// [7 * 3] 7
// the count = the distantce between window start and the target index
// O(n) O(n)

// use the index to replace the count, to hold the important onse
// [1]
// [2]
// [2(3), 3(-1)] 3
// [2, 3, 4] 3
// [5] 5
// [5, 6] 5
// [7] 6
// [8] 7

// check if we need to pop naturally or forcely 
var maxSlidingWindow = function(nums, k) {
    if (nums.length < k || k === 0) return []
    // naive solution
    const importantIndices = []
    const result = []
    for (let i = 0; i < nums.length; i++) {
        const item = nums[i]
        // put item into indices array by popping the smaller ones
        while (importantIndices.length > 0 
            && nums[importantIndices[importantIndices.length - 1]] <= item) {
            importantIndices.pop()
        }
        importantIndices.push(i)
        // [1, 2, 3], 3

        // need to pop one from left and collect the result
        if (i >= k) {
            if (i - k + 1 > importantIndices[0]) {
                importantIndices.shift()
            }
        }
        if (i >= k - 1) {
            result.push(nums[importantIndices[0]])
        }
      
    }
    
    return result
};
```
