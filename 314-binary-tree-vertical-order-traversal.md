Me explaining this on youtube: https://youtu.be/qsd5O9bjjK4

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
var verticalOrder = function(root) {
    if (root === null) return []
  
    // [9] [3, 15] [20] [7]
  
    // BFS, with queue
    // [node, index at the result]
    // a flag to determine index shifting
    const result = []
    const queue = [[root, 0]]
    while (queue.length > 0) {
      queue.push(null) // as ending identifier
      
      let isLeftNodeInserted = false
      let head
      
      // [[3]]
      // [[9], [3, 15], [20], [7]]
      while (head = queue.shift()) {
        const [node, index] = head
        if (index < 0) {
          isLeftNodeInserted = true
          result.unshift([])
        }
        
        const currentIndex = isLeftNodeInserted ? index + 1 : index
        
        if (!result[currentIndex]) {
          result[currentIndex] = [node.val]
        } else {
          result[currentIndex].push(node.val)
        }
        
        // children
        if (node.left) {
          queue.push([node.left, currentIndex - 1])
        }
        
        if (node.right) {
          queue.push([node.right, currentIndex + 1])
        }
      }
    }
  
    return result
};
```
