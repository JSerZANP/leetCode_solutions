Youtube explanation on this: https://youtu.be/JfWYJolU7RQ


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
var reverseList = function(head) {
    let start = null
    
    let p = head
    while (p) {
      const next = p
      p = p.next
      
      next.next = start
      start = next
    }
    
    return start
};
```
