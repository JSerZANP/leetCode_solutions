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
 * @param {number[]} preorder
 * @param {number[]} inorder
 * @return {TreeNode}
 */
var buildTree = function (preorder, inorder) {
  // [3,9,20,15,7]
  // 3 -> root current root
  // 9 -> left? right? 9 before 3 in inorder, so 9 is left child
  // 9 -> current root
  // 20 -> 20 after 9, so it must be on the right tree, 20 after 3 as well, so it is the right root of 3
  // 20 -> current root
  // 15, before 15 > left root
  // 7 after 20, so it must be the right root or right root of 3, but 3 already has right, so right of 20

  // [9,3,15,20,7]
  // thus we have an idea

  // 1. create nodes from pre-order
  // 2. for a node if its on the left, it is the left child
  // 3. for a node if it's on the right, it might be right child all of the paths
  // need to go through the path to root, stop when it is before a node or a node already has as right child

  // how do we get the parent node?
  // we can use array to hold the path, the top is the current node

  const path = [];
  const indexMap = new Map(
    [...inorder.entries()].map(([index, value]) => [value, index])
  );

  let root = null;
  for (const val of preorder) {
    const node = new TreeNode(val);
    if (path.length > 0) {
      const currentRoot = path.at(-1);
      if (indexMap.get(val) < indexMap.get(currentRoot.val)) {
        // left child

        path.at(-1).left = node;
      } else {
        // it could be right child of any node in the path
        // and we can pop the unused one.
        while (
          path.length > 1 &&
          indexMap.get(val) > indexMap.get(path.at(-2).val)
        ) {
          path.pop();
        }

        // now the top node is the parent of node
        path.at(-1).right = node;
        // once the right is set, we should remove it from the path
        // so that it never receives new right child
        path.pop();
      }
    } else {
      root = node;
    }
    path.push(node);
  }
  return root;
};
```
