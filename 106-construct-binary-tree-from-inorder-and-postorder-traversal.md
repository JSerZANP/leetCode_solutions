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
 * @param {number[]} inorder
 * @param {number[]} postorder
 * @return {TreeNode}
 */
var buildTree = function (inorder, postorder) {
  // [9,3,15,20,7]

  // [9,15,7,20,3]

  // the last item of postorder is the root
  // 3 - root
  // 20 ? left right?
  // 20 is after 3, so it is right node of 3
  // 7 after 20, so it is the right child of 7
  // 15 before 7, it might be left of 7, or 20, or 3

  const path = [];
  let root = null;

  const indexMap = new Map(
    [...inorder.entries()].map(([index, value]) => [value, index])
  );

  while (postorder.length > 0) {
    const val = postorder.pop();
    const node = new TreeNode(val);
    if (path.length === 0) {
      path.push(node);
      root = node;
    } else {
      if (indexMap.get(val) > indexMap.get(path.at(-1).val)) {
        // right child
        path.at(-1).right = node;
        path.push(node);
      } else {
        // it could be left of any child in the path
        while (
          path.length > 1 &&
          indexMap.get(val) < indexMap.get(path.at(-2).val)
        ) {
          path.pop();
        }

        path.at(-1).left = node;
        // once a node has left
        // it is safe to remove it from path
        // since in postorder, its right child is set before left child
        path.pop();
        path.push(node);
      }
    }
  }

  return root;
};
```
