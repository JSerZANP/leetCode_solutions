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
var getMinimumDifference = function (root) {
  // traverse it in an array
  // get the diff in O(n^2)

  // but we didn't use the fact it is BST
  // it is already ordered?

  // For BST
  // Inorder traversal leads to an ordered array

  // then the minimum diff should be two consecutive
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
  let min = Infinity;
  for (let i = 1; i < list.length; i++) {
    min = Math.min(list[i] - list[i - 1], min);
  }
  return min;
};
```
