My video of explanation: https://youtu.be/O0UuNAiy0yM


```js
/**
 * // Definition for a Node.
 * function Node(val, next, random) {
 *    this.val = val;
 *    this.next = next;
 *    this.random = random;
 * };
 */

/**
 * @param {Node} head
 * @return {Node}
 */
// Time: O(2n) => O(n)
// Space: O(n)
// var copyRandomList = function(head) {
//   // 2 pass
//   // 1. traverse all the nodes, clone them, put them into array
//   // 2 traverse all the nodes, set the random based on the index
  
  
//   const cloneMap = new Map()
  
//   const falseHead = new Node(0, head, null)
//   const falseHeadClone = new Node(0, null, null)
  
//   let p = falseHead
//   let pClone = falseHeadClone
  
//   while (p.next !== null) {
    
//     const clone = new Node(p.next.val, null, null)
    
//     cloneMap.set(p.next, clone)
    
//     pClone.next = clone
    
//     p = p.next
//     pClone = pClone.next
//   }

//   p = falseHead
//   pClone = falseHeadClone
  
//   while (p.next !== null) {
    
//     const clone = cloneMap.get(p.next)
//     clone.random = cloneMap.get(p.next.random)
    
//     p = p.next
//     pClone = pClone.next
//   }
  
//   return falseHeadClone.next
// };


// try to use 1 pass
// 
var copyRandomList = function(head) {
  // 2 pass
  // 1. traverse all the nodes, clone them, put them into array
  // 2 traverse all the nodes, set the random based on the index
  
  
  const cloneMap = new Map()
  
  const getClone = (node) => {
    if (node == null) return null
    if (cloneMap.has(node)) return cloneMap.get(node)
    
    const clone = new Node(node.val, null, null)
    cloneMap.set(node, clone)
    return clone
  }
  
  const falseHead = new Node(0, head, null)
  const falseHeadClone = new Node(0, null, null)
  
  let p = falseHead
  let pClone = falseHeadClone
  
  while (p.next !== null) {
    
    const clone = getClone(p.next)
    clone.random = getClone(p.next.random)
    pClone.next = clone
    
    p = p.next
    pClone = pClone.next
  }

 
  return falseHeadClone.next
};








```
