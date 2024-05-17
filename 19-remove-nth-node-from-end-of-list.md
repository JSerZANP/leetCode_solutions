A video explaining this: https://youtu.be/hyGN9Qp1tPU

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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  // scan it twice
  // first get the length -> l
  // then remove the l - n element
  // O(N + N - n) => O(2N)

  // or fast-slow cursor
  const start = new ListNode(null);
  start.next = head;

  let fast = start;
  while (n-- > 0) {
    fast = fast.next;
  }

  let slow = start;

  while (fast.next !== null) {
    fast = fast.next;
    slow = slow.next;
  }

  // remove the next of slow
  const target = slow.next;
  slow.next = target.next;
  target.next = null;

  return start.next;
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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  // need to find the item
  // keep track of the item before it

  const falseHead = new ListNode(0, head);
  let pPrev = falseHead;
  let pEnd = head;
  while (n > 1) {
    pEnd = pEnd.next;
    n -= 1;
  }
  while (pEnd.next != null) {
    pEnd = pEnd.next;
    pPrev = pPrev.next;
  }
  // pEnd stops at the last item
  // p stops at target
  pPrev.next = pPrev.next.next;
  return falseHead.next;
};
```
