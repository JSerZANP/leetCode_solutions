Here is me explaining it on youtube: https://youtu.be/Mf7PYwUvxBg

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */

// Time: O(n)
// Space: O(n) not O(3n)
// var lowestCommonAncestor = function(root, p, q) {
//     // return [LCA node, hasP, hasQ]
//     const walk = (node) => {
//       if (node === null) return [null, false, false]

//       const [LCALeft, leftHasP, leftHasQ] = walk(node.left)

//       if (LCALeft) {
//         return [LCALeft, true, true]
//       }

//       const [LCARight, rightHasP, rightHasQ] = walk(node.right)

//       if (LCARight) {
//         return [LCARight, true, true]
//       }

//       const hasP = leftHasP || rightHasP || node === p
//       const hasQ = leftHasQ || rightHasQ || node === q

//       if (hasP && hasQ) {
//         return [node, true, true]
//       } else {
//         return [null, hasP, hasQ]
//       }
//     }

//     return walk(root)[0]
// };

// Out of memory
// Time: O(3n) => O(n)
// Space: 1 + 2 + ... n = O(n ^ 2) plust O(n)
// var lowestCommonAncestor = function(root, p, q) {
//     // return the path to the node
//     const search = (node, target, path) => {
//       if (node === null) return null

//       if (node === target) return path.concat(target)

//       const leftSearched = search(node.left, target, path.concat(node))

//       if (leftSearched) return leftSearched

//       const rightSearched = search(node.right,target, path.concat(node))

//       return rightSearched
//     }

//     const pathP = search(root, p, [])
//     const pathQ = search(root, q, [])

//     let result
//     while(pathP[0] === pathQ[0]) {
//       result = pathP[0]
//       pathP.shift()
//       pathQ.shift()
//     }

//     return result
// };

// another way of global one path array
// Time: O(3n) => O(n)
// Space: O(n) + O(n) => O(n)
var lowestCommonAncestor = function (root, p, q) {
  // return the path to the node
  let path = [];
  const search = (node, target) => {
    if (node === null) return false;

    path.push(node);

    if (node === target) return true;

    const leftSearched = search(node.left, target);

    if (leftSearched) return true;

    const rightSearched = search(node.right, target);

    if (rightSearched) return true;

    path.pop();
  };

  search(root, p);
  const pathP = path;
  path = [];
  search(root, q);
  const pathQ = path;

  let result;
  while (pathP.length > 0 && pathQ.length > 0 && pathP[0] === pathQ[0]) {
    result = pathP[0];
    pathP.shift();
    pathQ.shift();
  }

  return result;
};
```

Another try

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function (root, p, q) {
  // path1
  // path2 O(n)

  // then find the last same item.
  const path = [];
  let path1;
  let path2;

  function walk(node) {
    if (node == null) return;
    path.push(node);
    if (node === p) {
      path1 = path.slice(0);
    }
    if (node === q) {
      path2 = path.slice(0);
    }
    if (node.left) {
      walk(node.left);
    }
    if (node.right) {
      walk(node.right);
    }
    path.pop();
  }
  walk(root);
  const index = path1.findLastIndex((item, i) => path1[i] === path2[i]);
  return path1[index];
};
```
