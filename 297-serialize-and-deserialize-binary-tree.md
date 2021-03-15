A video explaining this: https://youtu.be/BdYiijeQ680

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */

/**
 * Encodes a tree to a single string.
 *
 * @param {TreeNode} root
 * @return {string}
 */
var serialize = function(root) {
  if (root === null) return `[]`
  const result = []
  
  const queue = [root]
  while (queue.length > 0) {
    const head = queue.shift()
    result.push(head === null ? null : head.val)
    
    if (head) {
      queue.push(head.left)
      queue.push(head.right)
    }
  }
  
  // remove trailing null
  while (result[result.length - 1] === null) {
    result.pop()
  }

  return JSON.stringify(result)
};

/**
 * Decodes your encoded data to tree.
 *
 * @param {string} data
 * @return {TreeNode}
 */
var deserialize = function(data) {
  const arr = JSON.parse(data)
  if (!arr || arr.length === 0 || arr[0] === null) return null
  
  const top = new TreeNode(arr.shift())
  const prevLayer = [top]
  
  while (arr.length > 0) {
    const left = arr.shift() ?? null
    const right = arr.shift() ?? null
    const root = prevLayer.shift()
    
    const leftNode = left === null ? null : new TreeNode(left)
    root.left = leftNode
    const rightNode = right === null ? null : new TreeNode(right)
    root.right = rightNode
    
    if (left !== null) prevLayer.push(leftNode)
    if (right !== null) prevLayer.push(rightNode)
  }
  
  return top
};

/**
 * Your functions will be called as such:
 * deserialize(serialize(root));
 */
 ```
