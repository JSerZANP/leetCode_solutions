My video for this problem: https://youtu.be/P-YQOP47qBg
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
 * @param {number} x
 * @return {ListNode}
 */

// Time: O(n)
// Space: O(1)
var partition = function(head, x) {
    const start1 = new ListNode(0)
    const start2 = new ListNode(0)
    
    let p1 = start1
    let p2 = start2
    
    let p = head
    
    while (p) {
        if (p.val < x) {
           p1.next = p
           
           // cut p off 
           p = p.next
           p1.next.next = null
           p1 = p1.next 
        } else {
           p2.next = p
           
           // cut p off 
           p = p.next
           p2.next.next = null
           p2 = p2.next 
        }
    }
    
    p1.next = start2.next
    
    return start1.next
};
```
