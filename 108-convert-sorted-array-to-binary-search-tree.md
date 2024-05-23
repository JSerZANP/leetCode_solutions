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
 * @param {number[]} nums
 * @return {TreeNode}
 */
var sortedArrayToBST = function (nums) {
  // isn't enough we just form a triangle?
  // nope.
  // but it makes sens to choose the center as root
  // recursive

  // return the root
  function impl(i, j) {
    if (i > j) return null;
    const m = Math.floor((i + j) / 2);
    const root = new TreeNode(nums[m]);
    root.left = impl(i, m - 1);
    root.right = impl(m + 1, j);
    return root;
  }
  return impl(0, nums.length - 1);
};
```
