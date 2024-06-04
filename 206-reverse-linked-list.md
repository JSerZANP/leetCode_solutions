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
var reverseList = function (head) {
  let start = null;

  let p = head;
  while (p) {
    const next = p;
    p = p.next;

    next.next = start;
    start = next;
  }

  return start;
};
```

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
 * @return {ListNode}
 */
var reverseList = function (head) {
  // 1 2 3 4 5
  // p
  // 2 1 3 4 5

  let start = head;
  let p = head;
  while (p?.next != null) {
    const next = p.next;
    p.next = next.next;
    next.next = start;
    start = next;
  }
  return start;
};
```
