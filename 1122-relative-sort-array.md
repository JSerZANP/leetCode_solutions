Here is my video explaining this: https://youtu.be/FvOau8OlngI

```js
/**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @return {number[]}
 */
var relativeSortArray = function(arr1, arr2) {
  // 1. count numbers in arr1
  // 2. collect numbers in arr1 based on arr2
  // 3. append the rest numbers
  
  const count = new Map()
  for (let num of arr1) {
    if (count.has(num)) {
      count.set(num, count.get(num) + 1)
    } else {
      count.set(num, 1)
    }
  }
  
  const result = []
  
  for (let num of arr2) {
    if (count.has(num)) {
      let amount = count.get(num)
      while (amount > 0) {
        result.push(num)
        amount -= 1
      }
      count.delete(num)
    }
  }
  
  // the rest numbers 
  for (let num = 0; num <= 1000; num++) {
    if (count.has(num)) {
      let amount = count.get(num)
      while (amount > 0) {
        result.push(num)
        amount -= 1
      }
      count.delete(num)
    }
  }
  
  return result
};
```
