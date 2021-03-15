
Youtube video explaining this: https://youtu.be/q_lKF1XFF6M


```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode[]} lists
 * @return {ListNode}
 */
var mergeKLists = function(lists) {
    if (lists.length === 0) return null
    const merge2 = (list1, list2) => {
      const falseStart = new ListNode(0)
      
      let p = falseStart
      let p1 = list1
      let p2 = list2
      
      while (p1 && p2) {
        if (p1.val < p2.val) {
          p.next = p1
          p = p1
          p1 = p1.next
        } else {
          p.next = p2
          p = p2
          p2 = p2.next
        }
      }
      
      if (p1) {
        p.next = p1
      }
      
      if (p2) {
        p.next = p2
      }
      
      const result = falseStart.next
      falseStart.next = null
      return result
    }
    
    
    while (lists.length > 1) {
      let start = 0
      let end = lists.length - 1
      while (start < end) {
        lists[start] = merge2(lists[start], lists[end])
        start += 1
        end -= 1
      }
      
      lists.length = end + 1
    }
    
    return lists[0]
};
```
