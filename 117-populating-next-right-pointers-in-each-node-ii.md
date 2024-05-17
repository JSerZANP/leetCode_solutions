```js
/**
 * // Definition for a Node.
 * function Node(val, left, right, next) {
 *    this.val = val === undefined ? null : val;
 *    this.left = left === undefined ? null : left;
 *    this.right = right === undefined ? null : right;
 *    this.next = next === undefined ? null : next;
 * };
 */

/**
 * @param {Node} root
 * @return {Node}
 */
var connect = function (root) {
  if (root == null) return root;
  // BFS
  // each time we process layer by layer
  // and set up next

  const queue = [root];
  while (queue.length > 0) {
    let count = queue.length;
    let prev = null;
    while (count > 0) {
      const head = queue.shift();
      if (prev == null) {
        prev = head;
      } else {
        prev.next = head;
        prev = head;
      }

      if (head.left) {
        queue.push(head.left);
      }

      if (head.right) {
        queue.push(head.right);
      }
      count -= 1;
    }
  }
  return root;
};
```
