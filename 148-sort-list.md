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

// O(n^2) TLE
// var sortList = function(head) {
//     //  -> 4 2 1 3
//     // p  p1 p2

//     // -> 2 4 1 3
// //    p     p1p2
//     // -> 1 2 4 3
//     //      p p1p2
//     // -> 1 -> 2 -> 3 -> 4
//     //    p
//     // two pointers
//     // each round try to put the right node at the correct position
//     const falseHead = new ListNode(null, head)

//     // p.next should be where to put next smallest
//     let p = falseHead

//     while (p.next != null) {
//         let p1 = p.next
//         let p2 = p1.next
//         while (p2 != null) {
//             if (p2.val < p.next.val) {
//                 p1.next = p2.next
//                 p2.next = p.next
//                 p.next = p2
//                 p2 = p1.next
//             } else {
//                 p2 = p2.next
//                 p1 = p1.next
//             }
//         }
//         p = p.next
//     }

//     return falseHead.next
// };

//
var sortList = function (head) {
  if (head == null) return null;
  // are we able to improve it to O(nlogn)?
  // if list is of length two: constant time to sort
  // split the list into twos linear time

  // 4 2 1 3
  // [2, 4] [1, 3]

  // then merge the items
  // this is linear time.

  //     n items
  // O(2) * O(logn)
  // each item it is merged logn times

  // O(n logn)

  // split it in half
  // [2, 4] [1, 3] merge it

  // merge sort
  return mergeSort(head);
};

function mergeSort(head) {
  // split the list into two
  // sort them separately
  // merge them back

  // [start, end]

  // to find the middle, use two pointers
  let p1 = head;
  let p2 = head.next;
  while (p2?.next) {
    p1 = p1.next;
    p2 = p2.next.next ?? p2.next;
  }

  // if there is only one item
  if (p1.next == null) {
    return p1;
  }

  // break it up
  const next = p1.next;
  p1.next = null;
  // head and p1.next are new heads
  let start1 = mergeSort(head);
  let start2 = mergeSort(next);
  const falseHead = new ListNode();
  let p = falseHead;
  while (start1 != null && start2 != null) {
    if (start1.val <= start2.val) {
      p.next = start1;
      start1 = start1.next;
    } else {
      p.next = start2;
      start2 = start2.next;
    }
    p = p.next;
  }
  if (start1) {
    p.next = start1;
  }
  if (start2) {
    p.next = start2;
  }
  return falseHead.next;
}
```
