me explaining this on youtube: https://youtu.be/mvPR0p0WGe8

```js
/**
 * @param {number[]} nums
 * @param {number} k
 * @return {number}
 */

// Time: O(n log n)
// var findKthLargest = function(nums, k) {
//     // sort first
//     nums.sort((a, b) => b - a)
//     return nums[k - 1]
// };


// 3, 2, 1, 5, 6, 4
// 3, 5, 6, 4, 2, 1
// 4, 5, 6, 3, 2, 1
// 5, 6, 4, 3, 2, 1
// 6, 5, 4, 3, 2, 1

// fast short-circuit with quick sort
// Time: O(n ^ 2), average: n ( 1 + 1/2 + 1/4) = 
// 1 + 1 / 2 + 1 /2 ^ 2 + ..+ 1 / 2 ^ n = s
// 1/2 + 1/2 ^ 2 ... 1/2 ^ n + 1/2^n +1 = s/2
// 1 - 1/2^(n + 1) = s/2
// s = 2 - 1/2^n
// ns = 2n - n/2^n
// ~O(n)
// Space: O(1)
var findKthLargest = function(nums, k) {
  
  // use quick sort
  // if pivot happen to be the k-th, just return
  // if not, search half of them
  
  let start = 0
  let end = nums.length - 1
  
  
  const swap = (i, j) => {
    [nums[i], nums[j]] = [nums[j], nums[i]]
  }
  
  // [1, 5, 4, 2]
  // 
  while (start <= end) {
    const pivot = nums[start]
    let indexToSwap = start + 1
    
    for (let i = start + 1; i <= end; i++) {
      if (nums[i] >= pivot) {
        swap(indexToSwap, i)
        indexToSwap += 1
      }
    }
    
    swap(start, indexToSwap - 1)
    
    if (indexToSwap - 1 === k - 1) {
      return pivot
    }
    
    if (indexToSwap - 1 < k - 1) {
      start = indexToSwap
    } else {
      end = indexToSwap - 2
    }
  }
}

```
