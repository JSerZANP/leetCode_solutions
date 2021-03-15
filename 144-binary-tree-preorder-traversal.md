Here is my video of explainining it: https://youtu.be/u4O5XqBti2I
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
 * @return {number[]}
 */
var preorderTraversal = function(root) {
    const result = []
    
    if (root === null) return result
  
    const stack = [root]
    
    while (stack.length) {
      const top = stack.pop()
      result.push(top.val)
      if (top.right) stack.push(top.right)
      if (top.left) stack.push(top.left)
    }
  
    return result
}
```
