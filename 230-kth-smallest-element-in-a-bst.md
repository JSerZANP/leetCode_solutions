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
 * @param {number} k
 * @return {number}
 */
var kthSmallest = function (root, k) {
  // traverse it in an array
  const list = [];
  const walk = (node) => {
    if (node == null) return;
    if (node.left) {
      walk(node.left);
    }
    list.push(node.val);
    if (node.right) {
      walk(node.right);
    }
  };
  walk(root);
  return list[k - 1];
};
```
