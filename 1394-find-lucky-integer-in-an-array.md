Me explaining it on youtube: https://youtu.be/wSqQmPBN8uY

```js
/**
 * @param {number[]} arr
 * @return {number}
 */

// Time: O(n)
// Space: O(n)
// var findLucky = function(arr) {
//     // count all and find the largest luck number
//     const countMap = new Map()
//     for (let num of arr) {
//       if (countMap.has(num)) {
//         countMap.set(num, countMap.get(num) + 1)
//       } else {
//         countMap.set(num, 1)
//       }
//     }
  
//     let max = -1
    
//     for (let [num, count] of countMap) {
//       if (num === count && num > max) {
//         max = num
//       }
//     }
  
//     return max
// };

// sort first
// Time: O(n log n)
// Space: O(1)
var findLucky = function(arr) {
   arr.sort((a, b) => b - a)
  
   // 1, 2, 2, 3, 3
   // check at arr[arr[0]] !== , and arr[arr[0] - 1] === arr[0]
  
   // 4 3 2 2
   let max = -1
   let i = 0
   while (i < arr.length) {
     const num = arr[i]
     if (arr[i + num - 1] === num && arr[i + num] !== num) {
       max = num
       break
     }
     // if not move to the next different number
     i += 1
     while (arr[i] === num) {
       i += 1
     }
   }
  
   return max
};
```
