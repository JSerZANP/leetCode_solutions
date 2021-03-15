A video explaining this on youtube: https://youtu.be/lrrM8yXSSiA

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
// Time: O(n)
// Space: O(1)
var deleteDuplicates = function(head) {
    if (head === null) return null
    
    let p1 = head.next
    
    const newStart = new ListNode(0)
    newStart.next = head
    let p2 = head
    
    while (p1) {
        if (p1.val === p2.val) {
            // skip
        } else {
            p2.next = p1
            p2 = p2.next
        }
        p1 = p1.next
    }
    
    p2.next = null
    
    return newStart.next
};
```
