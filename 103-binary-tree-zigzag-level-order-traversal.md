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
var zigzagLevelOrder = function (root) {
  if (root == null) return [];

  const queue = [root];
  let direction = "right";
  const result = [];
  while (queue.length > 0) {
    let count = queue.length;
    let levelList = [];
    while (count > 0) {
      const head = queue.shift();
      levelList.push(head.val);
      if (head.left) {
        queue.push(head.left);
      }
      if (head.right) {
        queue.push(head.right);
      }
      count -= 1;
    }
    if (direction === "left") {
      levelList.reverse();
    }
    result.push(levelList);
    direction = direction === "right" ? "left" : "right";
  }
  return result;
};
```
