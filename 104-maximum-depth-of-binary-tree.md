Here is my explaining video on this: https://youtu.be/hIXFN-GD754


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
 * @return {number}
 */

// recursion
// TIME: O(n)
// Space: stack of Math.max call, longest path to leaf, worst O(n), O(log(n))
// var maxDepth = function(root) {
//     const _maxDepth = (node) => {
//       if (node === null) {
//         return 0
//       }
      
//       return Math.max(_maxDepth(node.left), _maxDepth(node.right)) + 1
//     }
    
//     return _maxDepth(root)
// };


// BFS time: O(n)  space O(n/2) O(n)
// var maxDepth = function(root) {
//     if (root === null) return 0
  
//     let depth = 0
//     const q = [root]
    
//     while (q.length > 0) {
//       q.push(null)
      
//       let item 
//       while (item = q.shift()) {
//         if (item.left) q.push(item.left)
//         if (item.right) q.push(item.right)
//       }
//       depth += 1
//     }
  
//     return depth
// };

// DFS time: O(n)  space O(n/2) O(log(n))
var maxDepth = function(root) {
    if (root === null) return 0
  
    let maxDepth = 0
    const stack = [[root, 1]]
    
    while (stack.length > 0) {
      const [top, currentDepth] = stack.pop()
    
      // leaf node
      if (!top.left && !top.right) {
        maxDepth = Math.max(maxDepth, currentDepth)
      }
      
      // if not leaf node
      if (top.left) stack.push([top.left, currentDepth + 1])
      if (top.right) stack.push([top.right, currentDepth + 1])
    }
  
    return maxDepth
};
```
