Here is a video explaining this : https://youtu.be/yHEU5xuGWdo

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
    
    let tmp = [head, 1]
    let p1 = head.next
    
    const newStart = new ListNode(0)
    let p2 = newStart
    
    while (p1) {
        if (p1.val === tmp[0].val) {
            tmp[1] += 1
        } else {
            if (tmp[1] === 1) {
                p2.next = tmp[0]
                p2 = p2.next
            }
            tmp = [p1, 1]
        }
        p1 = p1.next
    }
    
    if (tmp[1] === 1) {
        p2.next = tmp[0]
        p2.next.next = null
    } else {
        p2.next = null   
    }
    
    return newStart.next
};
```
