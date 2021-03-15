Here is a video of me explaining this: https://youtu.be/XH2lABHDeQ0


```js
/**
 * @param {number[]} arr
 * @param {number} k
 * @return {number[]}
 */
// Time: O(2nlogn + k) => O(nlogn)
// space: O(1)
// var getStrongest = function(arr, k) {
//     // 1. get the median
//     arr.sort((a, b) => a - b)
//     const median = arr[Math.floor((arr.length - 1) / 2)]
//     // 2. get the top k
//     arr.sort((a, b) => {
//       const diffA = Math.abs(a - median)
//       const diffB = Math.abs(b - median)
//       if (diffA < diffB) {
//         return 1
//       } else if (diffA > diffB) {
//         return -1
//       } else {
//         return b - a
//       }
//     })
  
//     return arr.slice(0, k)
// };


class PriorityQueue {
  // items is ordered as a min heap, children bigger than parent
  // index i childrend would be at index 2i  2i + 1
  // avoid using first element for easier index
  items = [undefined];

  get size() {
    return this.items.length - 1;
  }

  constructor(compare) {
    this.compare = compare;
  }

  peek() {
    return this.items[1]
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
    if (this.size === 0) {
      return result
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


var getStrongest = function(arr, k) {
  // get median through quick select
  let start = 0
  let end = arr.length - 1
  let medianIndex = Math.floor((start + end) / 2)
  let median
  
  // O(nlogn) => O(n^2)
  while (start <= end) {
     const pivot = arr[start]
     let indexToSwap = start + 1
     for (let i = start + 1; i <= end; i++) {
       if (arr[i] < pivot) {
         [arr[indexToSwap], arr[i]] = [arr[i], arr[indexToSwap]]
         indexToSwap += 1
       }
     }
     [arr[indexToSwap - 1], arr[start]] = [arr[start], arr[indexToSwap - 1]]
     
     if (indexToSwap - 1 === medianIndex) {
       median = arr[medianIndex]
       break
     } else if (indexToSwap - 1 < medianIndex) {
       start = indexToSwap - 1 + 1
     } else {
       end = indexToSwap - 1 - 1
     }
  }
  
  // O(nlogk)
  const pq = new PriorityQueue((a, b) => {
    const diffA = Math.abs(a - median)
    const diffB = Math.abs(b - median)
    if (diffA < diffB) {
      return -1
    } else if (diffA > diffB) {
      return 1
    } else {
      return a - b
    }
  })
  
  for (let num of arr) {
    pq.add(num)
    if (pq.size > k) {
      pq.poll()
    }
  }
  
  const result = []
  while (pq.size > 0) {
    result.push(pq.poll())
  }
  
  return result
}



```
