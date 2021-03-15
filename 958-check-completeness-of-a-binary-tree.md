Here is my video explaining this: https://youtu.be/jB0CeVd312M

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
 * @return {boolean}
 */

// Time: O(N)
// space: O(N/2) => O(N)
var isCompleteTree = function(root) {
    // BFS
  
    const queue = [root]
    
    let prevLevelNodeCount = 0
    let prevLevelNodeCounteExpected = 0
    
    while (queue.length > 0) {
      if (prevLevelNodeCount !== prevLevelNodeCounteExpected) {
        return false
      }
      
      prevLevelNodeCount = queue.length
      prevLevelNodeCounteExpected = prevLevelNodeCounteExpected === 0 ? 1 : prevLevelNodeCounteExpected * 2
      
      queue.push(null)
        
      let isNullMet = false
      let head
      while (head = queue.shift()) {
        if (head.left) {
          if (isNullMet) return false
          queue.push(head.left)
        } else {
          isNullMet = true
        }
        
        if (head.right) {
          if (isNullMet) return false
          queue.push(head.right)
        } else {
          isNullMet = true
        }
      }
    }
    
    return true
  
};
```
