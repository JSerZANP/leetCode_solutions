
Me explaining it : https://youtu.be/6zJt1tPj5OQ

```js
/**
 * // Definition for a Node.
 * function Node(val, next) {
 *     this.val = val;
 *     this.next = next;
 * };
 */

/**
 * @param {Node} head
 * @param {number} insertVal
 * @return {Node}
 */


// Time: O(n)
// Space: O(1)
var insert = function(head, insertVal) {
    // 1  [3  4]
    // 3 [4 1]
    // 4 [1 3]
  
    // [ 3 4] [4 3]
  
    // [3]
  
    // []
  
    // 1 handle special case for length 0, 1
    // 2. use two cursors to loop through all spaces betwen nodes
    //        if the range asc, check if insertVal falls in between
    //         if the range desc, check if insertVal is smaller than smaller, bigger than biggers
  
    // 1. create the node to insert
    const node = new Node(insertVal, null)
    
    if (head === null) {
      node.next = node
      return node
    }
  
    if (head.next === null) {
      head.next = node
      node.next = head
      return head
    }
  
  
    let p = head
    let pNext = head.next
    
    const insertAfter = (from, target) => {
      const next = from.next
      from.next = target
      target.next = next
    }
    
    do {
      // if it is asc, possible range to insert
      if (pNext.val >= p.val) {
        if (insertVal >= p.val && insertVal <= pNext.val) {
          insertAfter(p, node)
          break
        }
      } else {
        if (insertVal <= pNext.val || insertVal >= p.val) {
          insertAfter(p, node)
          break
        }
      }
      
      pNext = pNext.next
      p = p.next
      
      
      // if not inserted, measn all nodes are the same but not insertVal
      if (p === head) {
        // insert any where is fine
        insertAfter(p, node)
      }
      
    } while (p !== head)
    
    return head
};
      
      
      
      
      
      
      
```
