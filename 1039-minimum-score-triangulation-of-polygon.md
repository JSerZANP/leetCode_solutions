A video explaining this: https://youtu.be/NhgAG7QWk8k

```js
const minTri = (A, start, end, cache) => {
  const key = start * 100 + end
  if (cache[key]) {
    return cache[key]
  }
  
  const total = A.length
  
  const length = end - start + 1
  if (length < 3) return 0
  if (length === 3) return A[start] * A[start + 1] * A[end]
  
  let min = Infinity
  for (let i = start + 1; i < end; i++) {
    min = Math.min(
      min,
      minTri(A, start, i, cache) +
      minTri(A, i, end, cache) +
      A[start] * A[i] * A[end]
      )
  }
  cache[key] = min
  return min
}
/**
 * @param {number[]} A
 * @return {number}
 */
var minScoreTriangulation = function(A) {
    return  minTri(A, 0, A.length - 1, {})
};
```
