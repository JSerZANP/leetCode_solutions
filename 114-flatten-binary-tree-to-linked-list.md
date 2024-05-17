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
var flatten = function (root) {
  if (root === null) return null;

  const stack = [];
  if (root.right) stack.push(root.right);
  if (root.left) stack.push(root.left);

  let p = root;

  while (stack.length > 0) {
    const top = stack.pop();
    if (top.right) stack.push(top.right);
    if (top.left) stack.push(top.left);
    p.right = top;
    p.left = null;
    p = top;
  }
};
```

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
// O(n) space
// var flatten = function(root) {
//     if (root == null) return null
//     const path = []
//     const walk = (node) => {
//         if (node == null) {
//             return
//         }
//         path.push(node)
//         walk(node.left)
//         walk(node.right)
//     }
//     walk(root)
//     path.reduce((a, b) => {
//         a.right = b
//         a.left = null
//         return b
//     },)
// };

// we can use left to store the nodes temporarily
var flatten = function (root) {
  if (root == null) return null;
  let prev = null;

  const walk = (node, callback) => {
    if (node == null) {
      return;
    }
    callback(node);
    walk(node.left, callback);
    walk(node.right, callback);
  };

  walk(root, (node) => {
    if (prev == null) {
      prev = node;
    } else {
      prev.left = node;
      prev = node;
    }
  });

  walk(root, (node) => {
    node.right = node.left;
    node.left = null;
  });
};
```
