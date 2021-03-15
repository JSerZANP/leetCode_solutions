Here is my youtube video explaining this: https://youtu.be/Za9D1M0D0yw

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
var averageOfLevels = function(root) {
    // BFS
    const result = []
    const queue = [root]
    
    while (queue.length > 0) {
      
      const length = queue.length
      let sum = 0
      
      
      queue.push(null)
      
      let head
      while (head = queue.shift()) {
        sum += head.val
        
        if (head.left) queue.push(head.left)
        if (head.right) queue.push(head.right)
      }
      
      result.push(sum / length)
    }
  
    return result
};
```
