Here is my youtube video: https://youtu.be/ZaeKTYq9HVE


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
 * @return {void} Do not return anything, modify root in-place instead.
 */
var flatten = function(root) {
  if (root === null) return null
  
  const stack = []
  if (root.right) stack.push(root.right)
  if (root.left) stack.push(root.left)
  
  let p = root
  
  while (stack.length > 0) {
    const top = stack.pop()
    if (top.right) stack.push(top.right)
    if (top.left) stack.push(top.left)
    p.right = top
    p.left = null
    p = top
  }
};
```
