```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
var addTwoNumbers = function (l1, l2) {
  let carryover = 0;
  let p1 = l1;
  let p2 = l2;
  let falseHead = new ListNode(0);
  let p3 = falseHead;
  while (p1 != null || p2 != null) {
    let sum = (p1?.val ?? 0) + (p2?.val ?? 0) + carryover;
    if (sum > 9) {
      sum -= 10;
      carryover = 1;
    } else {
      carryover = 0;
    }
    const next = new ListNode(sum);
    p3.next = next;
    p3 = next;

    p1 = p1?.next;
    p2 = p2?.next;
  }

  if (carryover) {
    const next = new ListNode(1);
    p3.next = next;
  }

  return falseHead.next;
};
```
