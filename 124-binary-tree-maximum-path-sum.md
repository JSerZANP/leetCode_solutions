Here is the video for this problem: https://youtu.be/tZrhPNubBJk

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

// Time: O(n)
// Time: O(n)
// var maxPathSum = function(root) {

//     // return [max, maxConnected]
//     const walk = (node) => {
//       if (node === null) return [-Infinity, -Infinity]

//       const [maxLeft, maxLeftConnected] = walk(node.left)
//       const [maxRight, maxRightConnected] = walk(node.right)

//       const maxConnected = Math.max(
//         node.val,
//         node.val + maxLeftConnected,
//         node.val + maxRightConnected
//         )

//       const max = Math.max(
//         maxLeft,
//         maxRight,
//         maxConnected,
//         node.val + maxLeftConnected + maxRightConnected
//       )

//       return [max, maxConnected]
//     }

//     return walk(root)[0]
// };

// Time: O(n)
// Space: O(n)
// var maxPathSum = function(root) {

//     let max = -Infinity

//     // return [max, maxConnected]
//     const walk = (node) => {
//       if (node === null) return -Infinity

//       const maxLeftConnected = walk(node.left)
//       const maxRightConnected = walk(node.right)

//       const maxConnected = Math.max(
//         node.val,
//         node.val + maxLeftConnected,
//         node.val + maxRightConnected
//         )

//       max = Math.max(
//         max,
//         maxConnected,
//         maxLeftConnected,
//         maxRightConnected,
//         node.val + maxLeftConnected + maxRightConnected
//       )

//       return maxConnected
//     }

//     walk(root)
//     return max
// };

var maxPathSum = function (root) {
  let max = -Infinity;

  const walk = (node) => {
    if (node === null) return -Infinity;

    const maxLeft = walk(node.left);
    const maxRight = walk(node.right);

    const maxConnected = Math.max(
      node.val,
      maxLeft + node.val,
      maxRight + node.val
    );

    max = Math.max(
      max,
      maxLeft,
      maxRight,
      maxConnected,
      node.val + maxLeft + maxRight
    );

    return maxConnected;
  };
  walk(root);
  return max;
};
```

Another try

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
var maxPathSum = function (root) {
  // suppose there is the longest path
  // what's special about it ?
  // for the root node
  // if the path has contains root node, then it must be the longest path on the left(which connects to root)
  // and also the same on the right
  // if not , then it must be the longest path on the sub tree

  // so
  // Max Root  = max{Max Left, Max Right, Max Left To Root + Max Right To Root}

  /**
   * @returns {[number, number]} [max, maxToRoot]
   */
  function walk(node) {
    if (node == null) {
      return [-Infinity, -Infinity];
    }

    const [maxLeft, maxLeftToRoot] = walk(node.left);
    const [maxRight, maxRightToRoot] = walk(node.right);

    const maxToRoot = Math.max(
      maxLeftToRoot + node.val,
      maxRightToRoot + node.val,
      node.val
    );

    const max = Math.max(
      maxLeft,
      maxRight,
      maxLeftToRoot + maxRightToRoot + node.val,
      maxToRoot
    );
    return [max, maxToRoot];
  }
  return walk(root)[0];
};
```
