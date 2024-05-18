Here is my video of explaining this problem: https://youtu.be/fetWW2iGU7k

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

// Time: O(n)
// Space: O(n) worst
// var rightSideView = function(root) {
//     if (root === null) return []

//     const result = []
//     // BFS => queue
//     const queue = [root]

//     while (queue.length > 0) {
//       // push a null as ending identifier
//       queue.push(null)

//       let rightMostVal
//       let head
//       while (head = queue.shift()) {
//         rightMostVal = head.val

//         if (head.left) queue.push(head.left)
//         if (head.right) queue.push(head.right)
//       }

//       result.push(rightMostVal)
//     }

//     return result
// };

// checking end of layer by index
// var rightSideView = function(root) {
//     if (root === null) return []

//     const result = []
//     // BFS => queue
//     const queue = [root]

//     while (queue.length > 0) {
//       // push a null as ending identifier
//       let countOfThisLayer = queue.length
//       let rightMostVal
//       while (countOfThisLayer > 0) {
//         const head = queue.shift()
//         rightMostVal = head.val

//         if (head.left) queue.push(head.left)
//         if (head.right) queue.push(head.right)

//         countOfThisLayer -= 1
//       }

//       result.push(rightMostVal)
//     }

//     return result
// };

var rightSideView = function (root) {
  if (root === null) return [];

  const queue = [root];

  const result = [];

  while (queue.length > 0) {
    queue.push(null);

    let rightMostVal = null;

    let head;
    while ((head = queue.shift())) {
      rightMostVal = head.val;

      if (head.left) {
        queue.push(head.left);
      }

      if (head.right) {
        queue.push(head.right);
      }
    }

    result.push(rightMostVal);
  }

  return result;
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
 * @return {number[]}
 */
var rightSideView = function (root) {
  if (root == null) return [];

  // BFS
  const queue = [root];
  const result = [];
  while (queue.length > 0) {
    let rightMost = null;
    let count = queue.length;
    while (count > 0) {
      const head = queue.shift();
      rightMost = head.val;

      if (head.left) {
        queue.push(head.left);
      }
      if (head.right) {
        queue.push(head.right);
      }
      count -= 1;
    }
    result.push(rightMost);
  }
  return result;
};
```
