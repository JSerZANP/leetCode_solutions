A video explaining this: https://youtu.be/I-GDJ0VrRXI

```js
/**
 * @param {string} path
 * @return {string}
 */
// var simplifyPath = function(path) {
//     return '/' + path.split('/').filter(item => !['', '.'].includes(item))
//       .reduce((arr, item) => {
//       if (item === '..') {
//         arr.pop()
//       } else {
//         arr.push(item)
//       }
//       return arr
//     }, []).join('/')
// };

var simplifyPath = function(path) {
    const chunk = []
    
    let lastSlashIndex = 0
    for (let i = 0; i < path.length + 1; i++) {
      const char = path[i]
      if ((i === path.length || char === '/')) {
        if (lastSlashIndex < i - 1) {
          const seg = path.slice(lastSlashIndex + 1, i)
          switch (seg) {
              case '..':
                chunk.pop()
                break
              case '.':
                break
            default:
              chunk.push(seg)
          }
        }
        lastSlashIndex = i
      }
    }
    
    return '/' + chunk.join('/')
};
```
