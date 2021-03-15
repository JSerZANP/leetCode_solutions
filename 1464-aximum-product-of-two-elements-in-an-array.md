Me explaining it on youtube: https://youtu.be/S3vgXAgFY6E


```js
/**
 * @param {number[]} nums
 * @return {number}
 */

// Time: O(n)
// space: O(2) => O(1)
// var maxProduct = function(nums) {
//     // get the top 2 largest numbers
//     const top2 = [-Infinity, -Infinity]
    
//     for (let num of nums) {
//       if (num >= top2[0]) {
//         top2[1] = top2[0]
//         top2[0] = num
//       } else if (num > top2[1]) {
//         top2[1] = num
//       }
//     }
  
//     return (top2[0] - 1) * (top2[1] - 1)
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

// Time: O(n)
// space: O(2) => O(1)
var maxProduct = function(nums) {
    // get the top 2 largest numbers
    const top2 = new PriorityQueue((a, b) => a - b)
    
    // O(2 * n * log2)
    for (let num of nums) {
      top2.add(num)
      if (top2.size > 2) {
        top2.poll()
      }
    }
  
    let product = 1
    // O(2 * log2)
    while (top2.size > 0) {
      product *= (top2.poll() - 1)
    }
  
    return product
};

```
