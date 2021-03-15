Me explaining this on youtube: https://youtu.be/SBwVTq3_X5o
```js
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
// var intersection = function(nums1, nums2) { // m n
//     // brute force
//     // m  *  n
    
//     // sort first
//     // m log m  + n log n + m + n
    
  
//     nums1.sort((a, b) => a - b)
//     nums2.sort((a, b) => a - b)
  
//     const result = []
  
//     while (nums1.length > 0 && nums2.length > 0) {
//       const head1 = nums1[0]
//       const head2 = nums2[0]
//       if (head1 === head2) {
//         result.push(head1)
        
//         while (nums1[0] === head1) {
//           nums1.shift()
//         }
        
//         while (nums2[0] === head1) {
//           nums2.shift()
//         }
//       } else {
//         if (head1 < head2) {
//           while (nums1[0] === head1) {
//             nums1.shift()
//           }
//         } else {
//           while (nums2[0] === head2) {
//             nums2.shift()
//           }
//         }
//       }
//     }
  
//     return result
// };


// Set
var intersection = function(nums1, nums2) { // m n
    const set1 = new Set(nums1)
    const set2 = new Set(nums2)
    const result = new Set()
    
    for (let num of set1) {
      if (set2.has(num)) {
        result.add(num)
      }
    }
  
  
    return [...result]
};
```
