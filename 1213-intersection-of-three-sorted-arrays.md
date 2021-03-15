Me explaining this on youtube: https://youtu.be/LY1DuGOH-gg


```js
/**
 * @param {number[]} arr1
 * @param {number[]} arr2
 * @param {number[]} arr3
 * @return {number[]}
 */
var arraysIntersection = function(arr1, arr2, arr3) {
  // brute force
  // suppose all n integers
  // O(n * lg(n) *2) => O(n * lg(n))
    
  // check the head until one is dead
  // pop(shift) the smaller ones
    
  // O(n)
  // O(n)
  const result = []
  
  while (arr1.length > 0 && arr2.length > 0 && arr3.length > 0) {
      const head1 = arr1[0]
      const head2 = arr2[0]
      const head3 = arr3[0]
      
      if (head1 === head2 && head1 === head3) {
          result.push(head1)
          arr1.shift()
          arr2.shift()
          arr3.shift()
      } else {
          //  1 1 2 
          //  1 2 2
          if (head1 <= head2 && head1 <= head3) {
              arr1.shift()
          }
          
          if (head2 <= head1 && head2 <= head3) {
              arr2.shift()
          }
          
          if (head3 <= head1 && head3 <= head2) {
              arr3.shift()
          }
      }
  }
  
  return result
};
```
