My video explaining it: https://youtu.be/NZFHcLdUgU0

```js
/**
 * // Definition for a Node.
 * function Node(val, neighbors) {
 *    this.val = val === undefined ? 0 : val;
 *    this.neighbors = neighbors === undefined ? [] : neighbors;
 * };
 */

/**
 * @param {Node} node
 * @return {Node}
 */

// Time: O(node count) 
// space: O(node count)

// BFS
// var cloneGraph = function(node) {
//     if (node === null) return null
//     // clone Map<node, clonedNode>
//     // traversed Set
    
//     // BFS to traverse the graph (use above Set to avoid circle)
//     // every time when process a node
//     //     check if it is already traversed
//     //     for each neighbor, 
//     //           if not cloned, create a new node
//     //           connected the node's clone
//     //           if it is not traversed
//     //               push the neighbor into the queue
//     // return the clonded input node
  
//     const clonedMap = new Map()
//     const traversed = new Set()
    
//     const queue = [node]
    
//     // clone the head
//     clonedMap.set(node, new Node(node.val))
    
//     while (queue.length > 0) {
//       const head = queue.shift()
//       if (traversed.has(head)) {
//         continue
//       }
      
//       const clonedHead = clonedMap.get(head)
      
//       for (let neighbor of head.neighbors) {
//         if (clonedMap.has(neighbor)) {
//           clonedHead.neighbors.push(clonedMap.get(neighbor))
//         } else {
//           const clonedNeighbor = new Node(neighbor.val)
//           clonedHead.neighbors.push(clonedNeighbor)
//           clonedMap.set(neighbor, clonedNeighbor)
//         }
        
//         // if it not traversed yet, queue it
//         if (!traversed.has(neighbor)) {
//           queue.push(neighbor)
//         }
//       }
      
      
//       traversed.add(head)
//     }
  
//     return clonedMap.get(node)
// };


var cloneGraph = function(node) {
    if (node === null) return null
    // clone Map<node, clonedNode>
    // traversed Set
    
    // BFS to traverse the graph (use above Set to avoid circle)
    // every time when process a node
    //     check if it is already traversed
    //     for each neighbor, 
    //           if not cloned, create a new node
    //           connected the node's clone
    //           if it is not traversed
    //               push the neighbor into the queue
    // return the clonded input node
  
    const clonedMap = new Map()
    const traversed = new Set()
    
    const stack = [node]
    
    // clone the head
    clonedMap.set(node, new Node(node.val))
    
    while (stack.length > 0) {
      const top = stack.pop()

      if (traversed.has(top)) {
        continue
      }
      
      const clonedHead = clonedMap.get(top)
      
      for (let neighbor of top.neighbors) {
        if (clonedMap.has(neighbor)) {
          clonedHead.neighbors.push(clonedMap.get(neighbor))
        } else {
          const clonedNeighbor = new Node(neighbor.val)
          clonedHead.neighbors.push(clonedNeighbor)
          clonedMap.set(neighbor, clonedNeighbor)
        }
        
        // if it not traversed yet, queue it
        if (!traversed.has(neighbor)) {
          stack.push(neighbor)
        }
      }
      
      
      traversed.add(top)
    }
  
    return clonedMap.get(node)
};










```
