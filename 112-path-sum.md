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
 * @param {number} targetSum
 * @return {boolean}
 */
var hasPathSum = function (root, targetSum) {
  if (root == null) return false;
  // DFS with a Sum
  const stack = [[root, 0]];
  while (stack.length > 0) {
    const [node, sum] = stack.pop();
    if (node.left != null) {
      stack.push([node.left, sum + node.val]);
    }
    if (node.right != null) {
      stack.push([node.right, sum + node.val]);
    }

    if (
      node.left == null &&
      node.right == null &&
      node.val + sum === targetSum
    ) {
      return true;
    }
  }
  return false;
};
```
