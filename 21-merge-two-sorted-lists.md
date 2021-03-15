A video explaining this: https://youtu.be/TDihxl5hs3E

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */

// Recursion
// Time: O(n)
// Space: O(n)
// var mergeTwoLists = function(l1, l2) {
//     if (l1 === null) return l2
//     if (l2 === null) return l1
  
//     if (l1.val <= l2.val) {
//       l1.next = mergeTwoLists(l1.next, l2)
//       return l1
//     } else {
//       l2.next = mergeTwoLists(l1, l2.next)
//       return l2
//     }
// };

// Iteration
// Time O(n)
// Space O(1)
var mergeTwoLists = function(l1, l2) {
    let head = new ListNode()
    let p = head
    
    while (l1 && l2) {
      console.log(l1.val, l2.val)
      if (l1.val <= l2.val) {
        p.next = l1
        l1 = l1.next
      } else {
        p.next = l2
        l2 = l2.next
      }
      p = p.next
    }
  
    if (l1) p.next = l1
    if (l2) p.next = l2
    
    return head.next
};
```
