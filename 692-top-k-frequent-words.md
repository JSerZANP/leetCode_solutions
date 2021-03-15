me explaining this on youtube https://youtu.be/0XgI2-2AYps

```js
/**
 * @param {string[]} words
 * @param {number} k
 * @return {string[]}
 */

// brute force solution with sort

// Time: O(nlogn)
// Space: O(n)
// var topKFrequent = function(words, k) {
//     // 1. use a Map to track the count of each word
//     // 2. use an array to hold the unique word
//     // 3. sort the unique words count > lexico
//     // 4. slice top k
  
//     // O(n)
//     const countMap = new Map()
    
//     // O(n)
//     const uniqueWords = []
    
//     for (let word of words) {
//       if (countMap.has(word)) {
//         countMap.set(word, countMap.get(word) + 1)
//       } else {
//         countMap.set(word, 1)
//         uniqueWords.push(word)
//       }
//     }
    
//     // O(nlogn)
//     uniqueWords.sort((word1, word2) => {
//       const count1 = countMap.get(word1)
//       const count2 = countMap.get(word2)
      
//       if (count1 < count2) {
//         return 1
//       } else if (count1 > count2) {
//         return -1
//       } else {
//         if (word1 === word2) {
//           return 0
//         } else if (word1 < word2) {
//           return -1
//         } else {
//           return 1
//         }
//       }
//     })
    
//     //O(k)
//     return uniqueWords.slice(0, k)
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


// use a priority queue
// Time: O((n + k) log K) => O(nlogK)
// Space: O(N)


//  if use a sorted array of length k
// couldn't be improved to this O(nlogK)
var topKFrequent = function(words, k) {
    // 1. use a Map to track the count of each word
    // 2. use an array to hold the unique word
    // 3. sort the unique words count > lexico
    // 4. slice top k
  
    // O(n)
    const countMap = new Map()
    
    // if we found a word should be put it in , push it, pop the smallest
    // keep the amount to k
    // final sort O(klogk)
  
    // O(n)
    for (let word of words) {
      if (countMap.has(word)) {
        countMap.set(word, countMap.get(word) + 1)
      } else {
        countMap.set(word, 1)
      }
    }
    
    // create a priority queue to get top k elements
    const pq = new PriorityQueue((word1, word2) => {
      const count1 = countMap.get(word1)
      const count2 = countMap.get(word2)
      
      if (count1 < count2) {
        return -1 
      } else if (count1 > count2) {
        return 1
      } else {
        if (word1 === word2) {
          return 0
        } else if (word1 < word2) {
          return 1
        } else {
          return -1
        }
      }
    })
    
    // O(n)
    for (let [word] of countMap) {
      // O(logK)
      pq.add(word)
      if (pq.size > k) {
        // O(logK)
        pq.poll()
      }
    }
    
    const result = []
    
    while (pq.size > 0) {
      result.push(pq.poll())
    }
    
    return result.reverse()
};
```
