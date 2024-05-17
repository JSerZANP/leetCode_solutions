Here is a video explaining this: https://youtu.be/Yb-u_KcH7-c

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
 * @param {number} m
 * @param {number} n
 * @return {ListNode}
 */
var reverseBetween = function (head, m, n) {
  // 1 2 3 4 5
  // 1 3 2 4 5
  // 1 4 3 2 5

  // find 1, find 2 find 5
  // insert 2->next after 1  , recursively.
  // until 5 is met

  const start = new ListNode(0);
  start.next = head;

  let pBefore = start;
  let pAfter = null;
  let pM = head;
  let pN = head;

  while (n > m) {
    pN = pN.next;
    n -= 1;
  }

  while (m > 1) {
    pM = pM.next;
    pN = pN.next;
    pBefore = pBefore.next;
    m -= 1;
  }

  pAfter = pN.next;
  // insert pM.next after pBefore
  while (pM.next != pAfter) {
    // cut off pM.next
    const node = pM.next;
    pM.next = node.next;

    // insert
    node.next = pBefore.next;
    pBefore.next = node;
  }

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
 * @param {number} left
 * @param {number} right
 * @return {ListNode}
 */
var reverseBetween = function (head, left, right) {
  //      2  ->     4
  // 1 -> 4 ->  3 -> 2  -> 5

  // need pointers
  // p1 -> move along the list
  // p2 -> the previous node of left

  // left might be head, so need a false head
  const falseHead = new ListNode(0, head);
  let shouldReverse = false;
  let p = falseHead;
  let p2 = falseHead;
  let index = 0;
  while (p.next != null) {
    // if next is target
    if (index + 1 === left) {
      p2 = p;
      p = p.next;
      index += 1;
      shouldReverse = true;
      continue;
    }
    // if done
    if (index === right) {
      break;
    }

    if (shouldReverse) {
      const pNext = p.next;
      const p2next = p2.next;
      p.next = pNext.next;

      p2.next = pNext;
      pNext.next = p2next;
      index += 1;
    } else {
      p = p.next;
      index += 1;
    }
  }
  return falseHead.next;
};
```
