A video explaining the details: https://youtu.be/issaJfZ82EU

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
 * @return {ListNode}
 */
var swapPairs = function(head) {
    // reverse the nodes after head
    const swap = (node) => {
      if (node && node.next && node.next.next) {
          const first = node.next
          const second = node.next.next
          first.next = second.next
          second.next = first
          node.next = second
        
          swap(first)
      }
    }
    
    const start = new ListNode(null)
    start.next = head
    swap(start)
  
    return start.next
};
```
