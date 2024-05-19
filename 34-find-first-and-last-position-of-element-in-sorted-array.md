Youtube video explaining this: https://youtu.be/umNimvLVruc

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */

// Time: O(2logN) => O(logN)
// Space: O(1)
// var searchRange = function(nums, target) {
//     // [S1...Sk], [target ..target], [Sl..Sn]

//     // mode 2 : return the range
//     // mode -1 : return the left boundary
//     // mode 1 : return the right boudary
//     const search  = (i, j, mode) => {
//       if (i > j) return [-1, -1]

//       const middle = Math.floor((i + j) / 2)

//       if (mode === 2) {
//         if (nums[middle] < target) {
//           return search(middle + 1, j, 2)
//         } else if (nums[middle] > target) {
//           return search(i, middle - 1, 2)
//         } else {
//           return [
//             search(i, middle, -1),
//             search(middle, j, 1)
//           ]
//         }
//       } else if (mode === -1) {
//         if (nums[middle] === target) {
//           if (middle === i || nums[middle - 1] !== target) {
//             return middle
//           } else {
//             return search(i, middle - 1, -1)
//           }
//         } else {
//           return search(middle + 1, j, -1)
//         }
//       } else if (mode === 1) {
//         if (nums[middle] === target) {
//           if (middle === j || nums[middle + 1] !== target) {
//             return middle
//           } else {
//             return search(middle + 1, j, 1)
//           }
//         } else {
//           return search(i, middle - 1,  1)
//         }
//       }
//     }

//     return search(0, nums.length - 1, 2)
// };

// Two Cursor Iteration
// Time: O(logN)
// Space: O(1)
// var searchRange = function(nums, target) {
//   let i = 0
//   let j = nums.length - 1

//   while (i <= j) {
//     const middle = Math.floor((i + j) / 2)
//     if (nums[middle] < target) {
//       i = middle + 1
//     } else if (nums[middle] > target) {
//       j = middle - 1
//     } else {
//       // find the left boundary
//       let k = middle
//       while (i <= k) {
//         const middleLeft = Math.floor((i + k) / 2)
//         if (nums[middleLeft] === target) {
//           if (middleLeft === i || nums[middleLeft - 1] !== target) {
//             i = middleLeft
//             break
//           } else {
//             k = middleLeft - 1
//           }
//         } else {
//           i = middleLeft + 1
//         }
//       }

//       // find the right boundary
//       let l = middle
//       while (l <= j) {
//         const middleRight = Math.floor((l + j) / 2)
//         if (nums[middleRight] === target) {
//           if (middleRight === j || nums[middleRight + 1] !== target) {
//             j = middleRight
//             break
//           } else {
//             l = middleRight + 1
//           }
//         } else {
//           j = middleRight -1
//         }
//       }

//       break
//     }
//   }

//   if (i <= j) {
//     return [i, j]
//   } else {
//     return [-1, -1]
//   }
// };

var searchRange = function (nums, target) {
  let i = 0;
  let j = nums.length - 1;

  while (i <= j) {
    const middle = Math.floor((i + j) / 2);
    if (nums[middle] < target) {
      i = middle + 1;
    } else if (nums[middle] > target) {
      j = middle - 1;
    } else {
      // find the left boundary
      let k = middle;
      while (i <= k) {
        const middleLeft = Math.floor((i + k) / 2);
        if (nums[middleLeft] === target) {
          k = middleLeft - 1;
        } else {
          i = middleLeft + 1;
        }
      }

      // find the right boundary
      let l = middle;
      while (l <= j) {
        const middleRight = Math.floor((l + j) / 2);
        if (nums[middleRight] === target) {
          l = middleRight + 1;
        } else {
          j = middleRight - 1;
        }
      }
      break;
    }
  }

  if (i <= j) {
    return [i, j];
  } else {
    return [-1, -1];
  }
};
```

Another try in 2024

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function (nums, target) {
  // search first index
  // and last index
  const first = searchFirst(nums, target);
  const last = searchLast(nums, target);
  return [first, last];
};

var searchFirst = function (nums, target) {
  let i = 0;
  let j = nums.length - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (target <= nums[m]) {
      j = m - 1;
    } else {
      i = m + 1;
    }
  }
  // it stops => j is not target, i might be target
  return nums[i] === target ? i : -1;
};

var searchLast = function (nums, target) {
  let i = 0;
  let j = nums.length - 1;
  while (i <= j) {
    const m = Math.floor((i + j) / 2);
    if (target >= nums[m]) {
      i = m + 1;
    } else {
      j = m - 1;
    }
  }
  // it stops => i is not target, j might be target
  return nums[j] === target ? j : -1;
};
```
