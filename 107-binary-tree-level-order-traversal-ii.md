Here is me explaining : https://youtu.be/-0i4BUs79ck


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
var levelOrderBottom = function(root) {
    if (root === null) return []
    const result = []
    
    const queue = [root]
    
    while (queue.length > 0) {
      queue.push(null)
      const layer = []
      let head
      while (head = queue.shift()){
        layer.push(head.val)
        if (head.left) queue.push(head.left)
        if (head.right) queue.push(head.right)
      }
      result.unshift(layer)
    }
  
    return result
};
```
