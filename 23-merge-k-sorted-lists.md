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
var mergeKLists = function (lists) {
  if (lists.length === 0) return null;
  const merge2 = (list1, list2) => {
    const falseStart = new ListNode(0);

    let p = falseStart;
    let p1 = list1;
    let p2 = list2;

    while (p1 && p2) {
      if (p1.val < p2.val) {
        p.next = p1;
        p = p1;
        p1 = p1.next;
      } else {
        p.next = p2;
        p = p2;
        p2 = p2.next;
      }
    }

    if (p1) {
      p.next = p1;
    }

    if (p2) {
      p.next = p2;
    }

    const result = falseStart.next;
    falseStart.next = null;
    return result;
  };

  while (lists.length > 1) {
    let start = 0;
    let end = lists.length - 1;
    while (start < end) {
      lists[start] = merge2(lists[start], lists[end]);
      start += 1;
      end -= 1;
    }

    lists.length = end + 1;
  }

  return lists[0];
};
```

Another try in 2024

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

// N list k items
// each item is merged logN times
// logN * k * N
var mergeKLists = function (lists) {
  if (lists.length === 0) return null;
  // we merge one after another
  // that means 1st list merged n - 1 times, 2nd n - 2 times
  // suppose list are all k numbers
  // k*(n-1) +k*(n -2) + k...(1)
  // O(n^2 * k)
  // we can also use k pointers to compare and merge them all together
  // O(N * k * N)

  // if we can merge them separately, two at a time
  // then for each item in a list, it could be merged O(logN times)
  // O(logN * N * K)

  while (lists.length > 1) {
    let i = 0;
    let j = lists.length - 1;
    while (i <= j) {
      lists[i] = merge(lists[i], lists[j]);
      i += 1;
      j -= 1;
    }
    // when stopped, i is at the non-existing position
    lists.length = i;
  }
  return lists[0];
};

function merge(list1, list2) {
  if (list1 === list2) return list1;

  const head = new ListNode();
  let p = head;
  let p1 = list1;
  let p2 = list2;
  while (p1 && p2) {
    if (p1.val <= p2.val) {
      p.next = p1;
      p1 = p1.next;
    } else {
      p.next = p2;
      p2 = p2.next;
    }
    p = p.next;
  }
  if (p1) {
    p.next = p1;
  }
  if (p2) {
    p.next = p2;
  }
  return head.next;
}
```
