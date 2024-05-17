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
var deleteDuplicates = function (head) {
  if (head === null) return null;

  let tmp = [head, 1];
  let p1 = head.next;

  const newStart = new ListNode(0);
  let p2 = newStart;

  while (p1) {
    if (p1.val === tmp[0].val) {
      tmp[1] += 1;
    } else {
      if (tmp[1] === 1) {
        p2.next = tmp[0];
        p2 = p2.next;
      }
      tmp = [p1, 1];
    }
    p1 = p1.next;
  }

  if (tmp[1] === 1) {
    p2.next = tmp[0];
    p2.next.next = null;
  } else {
    p2.next = null;
  }

  return newStart.next;
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
 * @return {ListNode}
 */
var deleteDuplicates = function (head) {
  // say [a, b] contains duplicates
  // we need to keep track of the node before it
  // sfor each node, we just check if there are duplicates following
  const falseHead = new ListNode(0, head);
  let p = falseHead; // 5

  while (p.next != null) {
    // 5
    let start = p.next; // 5
    let end = p.next; // 5
    while (end.next?.val === start.val) {
      end = end.next;
    }
    if (end != start) {
      p.next = end.next;
    } else {
      p = p.next;
    }
  }
  return falseHead.next;
};
```
