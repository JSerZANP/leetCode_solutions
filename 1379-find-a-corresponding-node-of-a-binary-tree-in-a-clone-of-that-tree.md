
Me explaining it on youtube: https://youtu.be/tP2nCq9L1PQ

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} original
 * @param {TreeNode} cloned
 * @param {TreeNode} target
 * @return {TreeNode}
 */
// Time: O(n)
// Space: height of tree O(height)
var getTargetCopy = function(original, cloned, target) {
    // 1. need to search target => O(n)
    // 2. pass down the corresponding node to the recursion
    
    const walk = (node, clonedNode, target) => {
      if (node === target) return clonedNode
      
      let result = null
      
      if (node.left !== null) {
        result = walk(node.left, clonedNode.left, target)
      }
      
      if (result !== null) return result
      
      if (node.right !== null) {
        result = walk(node.right, clonedNode.right, target)
      } 
      
      return result
    }
    
    return walk(original, cloned, target)
};
```
