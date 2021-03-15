A video explaining this problem: https://youtu.be/WAmjkVqH2go

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

const traverse = (node, currentSum) => {
     let sum = currentSum
     if (node.right) {
         sum = traverse(node.right, currentSum)
     }
     
     node.val = sum + node.val

     if (node.left) {
         sum = traverse(node.left, node.val)
         return sum
     }
    
     return node.val
}

/**
 * @param {TreeNode} root
 * @return {TreeNode}
 */
var bstToGst = function(root) {
    traverse(root, 0)
    return root
};
```
