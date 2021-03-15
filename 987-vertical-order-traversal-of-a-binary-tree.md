Here is me explaining it on youtube: https://youtu.be/_3d2umHh1Us


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
 * @return {number[][]}
 */
var verticalTraversal = function(root) {
    // [[3]]
    // [[9], [3], [20]]
  
    // queue Array<[node, index]>
    // insert an array at the resut if index < 0, and shift all the indexes of that layer.
    if (root === null) return []
  
    // [9] [3, 15] [20] [7]
  
    // BFS, with queue
    // [node, index at the result]
    // a flag to determine index shifting
    const result = []
    const queue = [[root, 0]]
    while (queue.length > 0) {
      queue.push(null) // as ending identifier
      
      let isLeftNodeInserted = false
      let head
      const diffMap = new Map()
      // [[3]]
      // [[9], [3, 15], [20], [7]]
      while (head = queue.shift()) {
        const [node, index] = head
        
        if (index < 0) {
          isLeftNodeInserted = true
        }
  
        
        if (!diffMap.has(index)) {
          diffMap.set(index, [])
        }
        
        diffMap.get(index).push(node.val)
        
        // children
        if (node.left) {
          queue.push([node.left, index - 1])
        }
        
        if (node.right) {
          queue.push([node.right, index + 1])
        }
      }
      
      
      if (isLeftNodeInserted) {
        result.unshift([])
      }
      // sort
      for (let [index, arr] of diffMap) {
        arr.sort((a, b) => a - b)
        
        const realIndex = isLeftNodeInserted ? index + 1 : index
        
        if (!result[realIndex]) {
          result[realIndex] = []
        }
        
        result[realIndex].push(...arr)
      }
      
      // update the child nodes which are already in the queue
      if (isLeftNodeInserted) {
        for (let element of queue) {
          element[1] += 1
        }
      }
    }
  
    return result
};
```
