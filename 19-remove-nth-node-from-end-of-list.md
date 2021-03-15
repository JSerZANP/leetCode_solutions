A video explaining this: https://youtu.be/hyGN9Qp1tPU

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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function(head, n) {
    // scan it twice
    // first get the length -> l
    // then remove the l - n element
    // O(N + N - n) => O(2N)
  
    // or fast-slow cursor
    const start = new ListNode(null)
    start.next = head
    
    let fast = start
    while (n-- > 0) {
      fast = fast.next
    }
  
    let slow = start
    
    while (fast.next !== null) {
      fast = fast.next
      slow = slow.next
    }
    
    // remove the next of slow
    const target = slow.next
    slow.next = target.next
    target.next = null
    
    return start.next
};
```
