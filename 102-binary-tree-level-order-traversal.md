me explaining this on youtube: https://youtu.be/4Lm0p0A2t1w
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
 * @return {number[][]}
 */

// Time: O(n)
// Space: O(n/2) => O(n)
var levelOrder = function(root) {
    if (root === null) return []
    
    const result = []
    // BFS
    const queue = [root]
    
    while (queue.length > 0) {
      queue.push(null)
      const level = []
      let head
      while (head = queue.shift()) {
        level.push(head.val)
        if (head.left) queue.push(head.left)
        if (head.right) queue.push(head.right)
      }
      result.push(level)
    }
  
    return result
};
```
