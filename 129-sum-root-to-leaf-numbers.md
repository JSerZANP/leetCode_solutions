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
 * @return {number}
 */
var sumNumbers = function (root) {
  // we can track the path during DFS
  // collect result when found leaf node
  let sum = 0;
  let currentSum = 0;
  const walk = (node) => {
    if (node == null) return;

    currentSum = currentSum * 10 + node.val;

    if (node.left == null && node.right == null) {
      sum += currentSum;
    }

    walk(node.left);
    walk(node.right);
    currentSum = (currentSum - node.val) / 10;
  };

  walk(root);

  return sum;
};
```
