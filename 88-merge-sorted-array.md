Video explaining this: https://youtu.be/dNDqJ-vtB18

```js
/**
 * @param {number[]} nums1
 * @param {number} m
 * @param {number[]} nums2
 * @param {number} n
 * @return {void} Do not return anything, modify nums1 in-place instead.
 */
var merge = function(nums1, m, nums2, n) {
  const totalLen = m + n
  
  let i = 0
  let j = 0
  
  while (j < nums2.length) {
    const index1 = m - 1 - i
    const index2 = n - 1 - j
    const index = m + n - 1 - (i + j)
    
    if (index1 > -1 && nums1[index1] >= nums2[index2]) {
      nums1[index] = nums1[index1]
      i += 1
    } else {
      nums1[index] = nums2[index2]
      j += 1
    }
  }
  
  return nums1
}
```
