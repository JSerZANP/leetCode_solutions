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
var partition = function (head, x) {
  const start1 = new ListNode(0);
  const start2 = new ListNode(0);

  let p1 = start1;
  let p2 = start2;

  let p = head;

  while (p) {
    if (p.val < x) {
      p1.next = p;

      // cut p off
      p = p.next;
      p1.next.next = null;
      p1 = p1.next;
    } else {
      p2.next = p;

      // cut p off
      p = p.next;
      p2.next.next = null;
      p2 = p2.next;
    }
  }

  p1.next = start2.next;

  return start1.next;
};
```

Another try

```js
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @param {number} x
 * @return {ListNode}
 */
var partition = function (head, x) {
  // 1 4 3 2 5 2

  // we can create two list and then combine them
  // 1 2 2
  // 4 3 5

  const falseHead1 = new ListNode(0);
  let p1 = falseHead1;
  const falseHead2 = new ListNode(0);
  let p2 = falseHead2;
  while (head != null) {
    const next = head.next;
    head.next = null;
    if (head.val < x) {
      p1.next = head;
      p1 = head;
    } else {
      p2.next = head;
      p2 = head;
    }
    head = head.next;
    head = next;
  }

  p1.next = falseHead2.next;
  return falseHead1.next;
};
```
