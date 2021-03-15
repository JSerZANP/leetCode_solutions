here is my video : https://youtu.be/NwyUsp7uGOk

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var countNodes = function(root) {
    // brute force: O(n) O(n)
    
    // O(height) => 2^h
  
    // binary search on 2^h numbers, check if exist
    // find the last element that exist
    
  
    // h * h => O(h^2) => O(logn * logn) => better than O(n)
    // space: O(logN)
  
    // 1. get the height
    let height = 0
    let p = root
    while (p) {
      height += 1
      p = p.left
    }
    
  
    const maxCountAtLastLayer = 2 ** (height - 1)
    
    let start = 0
    let end = maxCountAtLastLayer - 1
    
    while (start <= end) {
      const middle = Math.floor((start + end) / 2)
      if (isExit(middle)) {
        start = middle + 1
      } else {
        end -= 1
      }
      // end is what we want
    }
  
  
    function isExit(index) {
      const path = []
      while (path.length < height - 1) {
        if (index % 2 === 1) {
          path.push('right')
          index = (index - 1) / 2
        } else {
          path.push('left')
          index = index / 2
        }
      }
      
      // start from root to check the target node
      let start = root
      let branch
      while (branch = path.pop()) {
        start = start[branch]
        
        if (start === null) {
          return false
        }
      }
      
      return true
    }
  
    return maxCountAtLastLayer + end
};









```
