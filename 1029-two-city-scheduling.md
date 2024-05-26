Me explaining this: https://youtu.be/jZRI_eFwICk

```js
/**
 * @param {number[][]} costs
 * @return {number}
 */
class PriorityQueue {
  // items is ordered as a max heap, children bigger than parent
  // index i childrend would be at index 2i  2i + 1
  // avoid using first element for easier index
  items = [undefined];

  size() {
    return this.items.length - 1;
  }

  constructor(compare) {
    this.compare = compare;
  }

  add(element) {
    // put element at the end
    this.items.push(element);

    // recursively move it up to the root if it should be put ahead
    let i = this.items.length - 1;
    while (i > 1) {
      const parentIndex = Math.floor(i / 2);
      const compared = this.compare(this.items[parentIndex], element);
      if (compared <= 0) {
        break;
      }

      // move parent down
      this.items[i] = this.items[parentIndex];
      i = parentIndex;
    }

    this.items[i] = element;
  }

  _swap(i, j) {
    const temp = this.items[i];
    this.items[i] = this.items[j];
    this.items[j] = temp;
  }

  _exist(i) {
    return this.items[i] !== undefined;
  }

  poll() {
    // just get the top is ok

    let root = 1;
    const result = this.items[root];
    // set the last child to the root
    const newTop = this.items.pop();
    if (this.size() === 0) {
      return result;
    }

    this.items[root] = newTop;

    // move it down to the right position
    while (root < this.items.length) {
      let leftChildIndex = 2 * root;
      let rightChildIndex = 2 * root + 1;

      let shouldSwapLeft =
        this._exist(leftChildIndex) &&
        this.compare(newTop, this.items[leftChildIndex]) > 0;
      let shouldSwapRight =
        this._exist(rightChildIndex) &&
        this.compare(newTop, this.items[rightChildIndex]) > 0;

      if (!shouldSwapLeft && !shouldSwapRight) break;

      if (shouldSwapLeft && shouldSwapRight) {
        if (
          this.compare(
            this.items[leftChildIndex],
            this.items[rightChildIndex]
          ) <= 0
        ) {
          shouldSwapRight = false;
        } else {
          shouldSwapLeft = false;
        }
      }

      if (shouldSwapLeft) {
        this._swap(root, leftChildIndex);
        root = leftChildIndex;
      } else {
        this._swap(root, rightChildIndex);
        root = rightChildIndex;
      }
    }
    return result;
  }
}

// Time: O(nlogn)
var twoCitySchedCost = function (costs) {
  // sum all up to A
  // sort the people with cost[1] - cost[0] , asc
  // pick the top N peopl, update cost

  let minCost = 0;

  for (let cost of costs) {
    minCost += cost[0];
  }

  // use a priority queue to track the N people that should be set to B

  const pq = new PriorityQueue((a, b) => {
    return b[1] - b[0] - (a[1] - a[0]);
  });
  // O(2n)
  for (let i = 0; i < costs.length; i++) {
    pq.add(costs[i]);
    if (pq.size() > costs.length / 2) {
      pq.poll();
    }
  }

  while (pq.size() > 0) {
    const [toA, toB] = pq.poll();
    minCost += toB - toA;
  }

  return minCost;
};
```

Another try in 2024

```js
/**
 * @param {number[][]} costs
 * @return {number}
 */
var twoCitySchedCost = function (costs) {
  // 2n people to choose n people at A and n people at B
  // basically means if we all fly to A
  // how can I choose n people to fly to B to gain the best cost cut
  // we can sort and

  // first we fly to A
  const n = costs.length / 2;
  let totalCost = costs.reduce((a, b) => a + b[0], 0);

  // O(nlogn),O(n)
  const costGains = costs
    .map(([a, b]) => b - a)
    .sort((a, b) => a - b)
    .slice(0, n)
    .reduce((a, b) => a + b);

  // improve point: we don't need to sort the whole list
  // but choose the top N items
  // use quick sort => log2N => logN
  // or use Priority Queue to hold top N => O(n * logN)
  return totalCost + costGains;
};
```
