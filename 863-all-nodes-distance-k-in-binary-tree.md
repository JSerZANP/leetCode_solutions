Here is my video explaining this: https://youtu.be/SYOqAfwrb5g

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
 * @param {TreeNode} target
 * @param {number} K
 * @return {number[]}
 */

// time: O(n + n) => O(n)
// space: O(n)
var distanceK = function(root, target, K) {
    // 1. BFS on the children
    // 2. go up to k-th parent, for each parent, BFS on the other branch
    // to get up to k-th parent, DFS , keep the global stack
    const getPath = (root, target) => {
      
      const stack = []
      // 3 5 6
      // 3 5 null 2 null 4
      const pushStack = (node) => {
        while (node) {
          stack.push(node)
          node = node.left
        }
      }
      
      pushStack(root)
      
      while (stack.length > 0) {
        if (stack[stack.length - 1] === target) {
          break
        }
        
        const top = stack.pop()
        
        if (top === null) {
          stack.pop()
          continue
        }
        
        if (top.right) {
          stack.push(top)
          stack.push(null)
          pushStack(top.right)
        }
      }
      
      return stack.filter(item => item !== null)
    }
    
    // layer might be 0, means itself
    // root might be null
    const searchChildrenAtLayer = (root, layer) => {
      if (root === null || layer < 0) return []
      
      const queue = [root]
      while (queue.length > 0 && layer >= 0) {
        if (layer === 0) {
          return queue.map(node => node.val)
        }
        
        layer -= 1
        
        queue.push(null)
        let head
        while (head = queue.shift()) {
          if (head.left) queue.push(head.left)
          if (head.right) queue.push(head.right)
        }
      }
      
      return []
    }
    
    const result = []
    
    result.push(...searchChildrenAtLayer(target, K))
  
    const path = getPath(root, target)
  
    for (let i = 1; i <= K && path.length - 1 - i > -1; i++) {
      const parent = path[path.length - 1 - i]
      if (i === K) {
        result.push(parent.val)
        continue
      }
      
      const prev = path[path.length - 1 - i + 1]
      
      if (parent.left === prev) {
        result.push(...searchChildrenAtLayer(parent.right, K - i - 1))
      } else {
        result.push(...searchChildrenAtLayer(parent.left, K - i - 1))
      }
    }
  
    return result
};
```
