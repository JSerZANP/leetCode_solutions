My youtube video explaining this: https://youtu.be/3rVjpFVvVA8

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
var postorderTraversal = function(root) {
    const result = []
    
    if (root === null) return result
  
    const stack = []
    
    const pushStack = (node) => {
      while (node) {
        stack.push(node)
        node = node.left
      }
    }
    
    pushStack(root)
  
    while (stack.length > 0) {
      let top = stack[stack.length - 1]
      
      if (top === null) {
        stack.pop()
        top = stack.pop()
        result.push(top.val)
      } else {
        if (top.right) {
          stack.push(null)
          pushStack(top.right)
        } else {
          stack.pop()
          result.push(top.val)
        }
      }
    }
  
    return result
};
```
