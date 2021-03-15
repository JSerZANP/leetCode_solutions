Video explanation on this: https://youtu.be/gPuXCOrYIpg

```js
/**
 * @param {number} N
 * @return {number}
 */

const memo = (func) => {
  const cache = new Map()
  return function(...args) {
    const key = args.join('_')
    if (cache.has(key)) {
      return cache.get(key)
    }
    const result = func(...args)
    cache.set(key, result)
    return result
  }
}

var fib = memo((N) => {
  if (N === 0) return 0
  if (N === 1) return 1
  const result = fib(N - 1) + fib(N - 2)
  return result
})
```
