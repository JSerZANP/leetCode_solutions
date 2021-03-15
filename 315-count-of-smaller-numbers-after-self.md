Here is my video explaining this : https://youtu.be/JU0nukdutuo

```js
/**
 * @param {number[]} nums
 * @return {number[]}
 */

// time: O(n^2)
// space: O(n)
// var countSmaller = function(nums) {
//     // brute force: O(n^2)
  
//     // 5,2,6,1
    
//     // 1 2 5 6
  
//     // n * (logn  + n) => O(n ^ 2)
    
//     const result = [0]
    
//     const sorted = [nums[nums.length - 1]]
    
//     for (let i = nums[nums.length - 2]; i >= 0; i++) {
//       const num = nums[i]
      
//       let start = 0
//       let end = sorted.length - 1
      
//       while (start <= end) {
//         const middle = Math.floor((start + end) / 2)
//         if (sorted[middle] >= num) {
//           end -= 1
//         } else {
//           start += 1
//         }
//       }
      
//       // start is the insertion position
//       result.push(start)
      
//       // this cost O(n)
//       sorted.splice(start, 0, num)
//     }
  
//     return result.reverse()
// };


// possibly improved with BST
// O(Nlogn) ~ O(N^2)

class Node {
  constructor(val) {
    this.val = val
    this.countOfLeftTree = 0
    this.countOfSelf = 1
    this.left = null
    this.right = null
  }
}


// Time: O(nlogn) -> O(n^2)
// space: O(n)
var countSmaller = function(nums) {
  if (nums.length === 0) return []
  
  const root = new Node(nums[nums.length - 1])
  // return the smaller numbsers
  const searchAndInsert = (nodeVal) => {
    const node = new Node(nodeVal)
    let p = root
    let countOfSmaller = 0
    while (p) {
      if (node.val === p.val) {
        p.countOfSelf += 1
        return p.countOfLeftTree + countOfSmaller
      }
      
      if (node.val < p.val) {
        p.countOfLeftTree += 1
        if (p.left) {
          p = p.left
        } else {
          p.left = node
          return countOfSmaller
        }
      } else {
        countOfSmaller += p.countOfLeftTree + p.countOfSelf
        if (p.right) {
          p = p.right
        } else {
          p.right = node
          return countOfSmaller
        }
      }
    }
  }
  
  const result = [0]
  
  for (let i = nums.length - 2; i >= 0; i--) {
    result.push(searchAndInsert(nums[i]))
  }
  
  return result.reverse()
};

//          22(1, 1)
//    5(0,1)          52(2, 1)
//           23(0, 1)
```
