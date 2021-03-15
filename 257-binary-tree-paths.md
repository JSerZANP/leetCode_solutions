Here is my video explaining it: https://youtu.be/GfUmRahetKA

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
 * @return {string[]}
 */

// Time: O(n)
// Space: O(height of tree) O(n)
// var binaryTreePaths = function(root) {
//     if (root === null) return []
  
//     const result = []
    
//     const walk = (node, path) => {
//       const newPath = path === '' ? `${node.val}` : (path + '->' + node.val)
      
//       if (!node.left && !node.right) {
//         result.push(newPath)
//         return
//       }
      
//       if (node.left) walk(node.left, newPath)
//       if (node.right) walk(node.right, newPath)
//     }
    
//     walk(root, '')
    
//     return result
// };


// iteration

// [1, 2]
// [1, 2, null, 5]
// [1]
// [1, null, 3]
// time: O(n)
// space: O(height) O(n)
// var binaryTreePaths = function(root) {
//     if (root === null) return []
    
//     const result = []
    
//     const stack = []
    
//     const pushStack = (node) => {
//       while (node) {
//         stack.push(node)
//         node = node.left
//       }
//     }
    
//     const getCurrentPath = () => {
//       return stack.filter(item => item !== null).map(item => item.val).join('->')
//     }
    
//     pushStack(root)
    
//     while (stack.length > 0) {
//       let top = stack.pop()
      
//       if (top === null) {
//         top = stack.pop()
//         continue
//       }
      
//       if (!top.left && !top.right) {
//         const currentPath = getCurrentPath()
        
//         result.push(currentPath + (currentPath === '' ?  '' : '->') + top.val)
//         continue
//       }
      
//       if (top.right) {
//         stack.push(top)
//         stack.push(null)
//         pushStack(top.right)
//       }
//     }
  
//     return result
// };

// stack the path in
var binaryTreePaths = function(root) {
    if (root === null) return []
    
    const result = []
    
    // Array<node, prevPath>
    const stack = [[root, '']]
    
    while (stack.length > 0) {
      const [node, path] = stack.pop()
      
      const newPath = path + (path === '' ? '' : '->') + node.val
      if (!node.left && !node.right) {
        result.push(newPath)
      }
      
      if (node.left) {
        stack.push([node.left, newPath])
      }
      
      if (node.right) {
        stack.push([node.right, newPath])
      }
    }
    
    return result
};
```
