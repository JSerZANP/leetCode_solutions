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
 * @return {boolean}
 */
var hasCycle = function (head) {
  if (head == null) return false;
  let pSlow = head;
  let pFast = head;
  while (pFast != null) {
    pSlow = pSlow.next;
    pFast = pFast.next?.next;
    if (pSlow === pFast) {
      return true;
    }
  }
  return false;
};
```
