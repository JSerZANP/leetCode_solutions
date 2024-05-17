Here is an explanation video on this: https://youtu.be/hwG0ASauad8

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
 * @param {number} k
 * @return {ListNode}
 */
// slow and fast pointer, not available, because k might be > length
// O(2n)
// O(1)
var rotateRight = function (head, k) {
  if (head === null) return null;
  // get the length
  let length = 0;
  let p = head;
  while (p) {
    length += 1;
    p = p.next;
  }

  // avoid unnecessary loops
  k %= length;

  // new head would be length - k

  // add a new falst start node
  const start = new ListNode(0);
  start.next = head;

  let newHead;
  // the new head index would be length - k + 1
  // total would be length + 1
  p = start;
  let i = 0;

  while (i < length + 1) {
    if (i === length + 1 - 1) {
      p.next = head;
    }

    if (i === length - k + 1 - 1) {
      newHead = p.next;
      p.next = null;
      p = newHead;
    } else {
      p = p.next;
    }

    i += 1;
  }

  return newHead;
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
 * @param {number} k
 * @return {ListNode}
 */
var rotateRight = function (head, k) {
  if (head == null || k === 0) return head;
  // find the break point by two pointer
  // p
  // pEnd
  // then rotate it to move p.next to the head
  const falseHead = new ListNode(0, head);
  let p = falseHead;
  let pEnd = head;
  // this could be fafter by first getting the length and mod
  while (k > 1) {
    pEnd = pEnd.next;
    if (pEnd == null) {
      pEnd = head;
    }
    k -= 1;
  }
  while (pEnd.next != null) {
    pEnd = pEnd.next;
    p = p.next;
  }
  // pEnd stops at the last item
  // p stops at the item before the breakpoint
  const pNext = p.next;
  // cut it off first to avoid issue
  p.next = null;
  pEnd.next = falseHead.next;
  falseHead.next = pNext;
  return falseHead.next;
};
```
