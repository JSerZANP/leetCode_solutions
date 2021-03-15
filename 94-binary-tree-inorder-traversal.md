Here is me explaining this problem: https://youtu.be/BVY0SKdN0PM

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
var inorderTraversal = function(root) {
    const result = []
    if (root === null) return result
  
    const stack = []
    
    const pushStack = (node) => {
      while(node !== null) {
        stack.push(node)
        node = node.left
      }
    }
  
    pushStack(root)
  
    while(stack.length > 0) {
      const top = stack.pop()
      result.push(top.val)
      if (top.right) {
        pushStack(top.right)
      }
    }
  
    return result
};
```
