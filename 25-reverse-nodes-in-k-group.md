Youtube video to explain this : https://youtu.be/okUJJo2jV5k
```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
// TIME: O(2N)
// Space: O(1)
var reverseKGroup = function(head, k) {
    // reverse the list except the head
    const reverse = (node) => {
      // 1 - 2, 3, 4
      // 1 - 3, 2, 4
      // 1 - 4, 3, 2
      let p = node.next
      
      while (p.next) {
        const next = p.next.next
        
        p.next.next = node.next
        node.next = p.next
        p.next = next
      }
      
      return p
    }
    
    // swap k nodes, starting from node.next
    const swap = (node) => {
      if (node === null) return
      
      let count = 0
      let end = node.next
      while (end && count < k - 1) {
        count += 1
        end = end.next
      }
      
      // if there is enough k nodes
      if (end) {
        let next = end.next
        end.next = null
        
        // reverse the nodes and concat
        const newEnd = reverse(node)
        newEnd = next
        
        // continue
        swap(newEnd)
      }
    }
    
    const start = new ListNode()
    start.next = head
    
    swap(start)
  
    return start.next  
};
```
