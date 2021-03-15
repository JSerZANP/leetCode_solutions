My explaination here: https://youtu.be/aktWSwqhYRQ
```js
/**
 * @param {string[][]} paths
 * @return {string}
 */

// merge the paths
// Time: O(n^2)
// Space: O(1)
// var destCity = function(paths) {
//     while (paths.length > 1) {
//       const head = paths.shift()
      
//       for (let i = 0; i < paths.length; i++) {
//         // if they could be merged
//         if (head[0] === paths[i][1]) {
//           paths[i][1] = head[1]
//           break
//         }
        
//         if (head[1] === paths[i][0]) {
//           paths[i][0] = head[0]
//           break
//         }
//       }
//     }
//   return paths[0][1]
// };


// collect the result directly

// O(n) + worst O(n) => O(n)
// Space: O(n)
var destCity = function(paths) {
    
   const map = new Map(paths)
   
   for (let anyPath of map) {
     let start = anyPath[1]
     while (map.has(start)) {
       start = map.get(start)
     }
     
     return start
     break
   }
};
```
