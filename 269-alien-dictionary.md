My video of explaining this: https://youtu.be/d20ff5kVfo8

```js
/**
 * @param {string[]} words
 * @return {string}
 */

// Time: O(n ^ 2)  N-1 + n - 2 ...1
// Space: O(n ^ 2)
// var alienOrder = function(words) {    // m * n
//     // [t,f], [w, e], [r, t], [e, r]

//     // loop though all the words,
//            // collect the alphabets
//            // collect all the patsh, store paths as Map, and revere Map
//     // loop though all the letters
//     //    check if any path leading to it, by check the reverse Map
//     //    if no paths, collect it as result
//     //          remove the paths from Map and reverse Map
//     //    if no character collected, and there is still letters, invalid
//     // <from, Set<to>>
//     const forwardMap = new Map()
//     const backwardMap = new Map()
//     const alphabets = new Set()
//     // O(n)
//     for(let i = 0; i < words.length; i++) {

//       for(let j = 0; j < words[i].length; j++) {
//         //collect the alphabets
//         alphabets.add(words[i][j])
//       }

//       // compare with previous word to get the paths
//       if (i > 0) {
//         let j = 0
//         for (; j < words[i - 1].length && j < words[i].length; j++) {
//           const from = words[i - 1][j]
//           const to = words[i][j]

//           if (from != to) {
//             if (!forwardMap.has(from)) {
//               forwardMap.set(from, new Set())
//             }
//             forwardMap.get(from).add(to)

//             if (!backwardMap.has(to)) {
//               backwardMap.set(to, new Set())
//             }
//             backwardMap.get(to).add(from)

//             break
//           }
//         }

//         // invalid case
//         if (j === words[i].length && j !== words[i - 1].length) {
//           return ''
//         }
//       }
//     }

//     // now collect result
//     const result = []

//     while (alphabets.size > 0) {
//       let isHeadFound = false
//       // M * N
//       for (let char of alphabets) {
//         // if there is no path pointing to it, collect
//         if (!backwardMap.has(char)) {
//           result.push(char)
//           alphabets.delete(char)
//           isHeadFound = true
//           // update both maps

//           if (forwardMap.has(char)) {
//             const tos = forwardMap.get(char)

//             // delete char from reverse map of each to
//             // worst O(m * n - 1)
//             for (let to of tos) {
//               const froms = backwardMap.get(to)
//               froms.delete(char)

//               // if it is empty, remove it
//               if (froms.size === 0) {
//                 backwardMap.delete(to)
//               }
//             }

//             forwardMap.delete(char)
//           }

//         }
//       }

//       // invalid
//       if (!isHeadFound && alphabets.size > 0) {
//         return ''
//       }
//     }

//     return result.join('')
// };

// Time: O(n ^ 2)
// Space: O(n ^ 2)
// avoid keeping track of path heads
// var alienOrder = function(words) {    // m * n
//     // [t,f], [w, e], [r, t], [e, r]

//     // loop though all the words,
//            // collect the alphabets
//            // collect all the patsh, store paths as Map, and revere Map
//     // loop though all the letters
//     //    check if any path leading to it, by check the reverse Map
//     //    if no paths, collect it as result
//     //          remove the paths from Map and reverse Map
//     //    if no character collected, and there is still letters, invalid
//     // <from, Set<to>>
//     const forwardMap = new Map()

//     // <chara, count of paths leading to it>
//     const inboundCountMap = new Map()
//     const alphabets = new Set()
//     // O(n)
//     for(let i = 0; i < words.length; i++) {

//       for(let j = 0; j < words[i].length; j++) {
//         //collect the alphabets
//         alphabets.add(words[i][j])
//       }

//       // compare with previous word to get the paths
//       if (i > 0) {
//         let j = 0
//         for (; j < words[i - 1].length && j < words[i].length; j++) {
//           const from = words[i - 1][j]
//           const to = words[i][j]

//           if (from != to) {
//             if (!forwardMap.has(from)) {
//               forwardMap.set(from, new Set())
//             }

//             if (!forwardMap.get(from).has(to)) {
//               forwardMap.get(from).add(to)
//                if (!inboundCountMap.has(to)) {
//                 inboundCountMap.set(to, 0)
//               }
//               inboundCountMap.set(to, inboundCountMap.get(to) + 1)

//             }
//             break
//           }
//         }

//         // invalid case
//         if (j === words[i].length && j !== words[i - 1].length) {
//           return ''
//         }
//       }
//     }

//     // now collect result
//     const result = []

//     while (alphabets.size > 0) {
//       let isHeadFound = false
//       // M * N
//       for (let char of alphabets) {
//         // if there is no path pointing to it, collect
//         if (!inboundCountMap.has(char)) {
//           result.push(char)
//           alphabets.delete(char)
//           isHeadFound = true
//           // update both maps

//           if (forwardMap.has(char)) {
//             const tos = forwardMap.get(char)

//             // delete char from reverse map of each to
//             // worst O(m * n - 1)
//             for (let to of tos) {
//               inboundCountMap.set(to, inboundCountMap.get(to) - 1)
//               // if it is empty, remove it
//               if (inboundCountMap.get(to) === 0) {
//                 inboundCountMap.delete(to)
//               }
//             }

//             forwardMap.delete(char)
//           }

//         }
//       }

//       // invalid
//       if (!isHeadFound && alphabets.size > 0) {
//         return ''
//       }
//     }

//     return result.join('')
// };

var alienOrder = function (words) {
  const letters = new Set();

  // Map<letter, Set<letter>>
  const forwardMap = new Map();
  const backwardMap = new Map();

  const setForward = (from, to) => {
    if (forwardMap.has(from)) {
      forwardMap.get(from).add(to);
    } else {
      forwardMap.set(from, new Set([to]));
    }

    if (backwardMap.has(to)) {
      backwardMap.get(to).add(from);
    } else {
      backwardMap.set(to, new Set([from]));
    }
  };

  // find the first different letter, that is the relation
  // return if valid or not
  const collectForward = (word1, word2) => {
    let i = 0;
    for (; i < word1.length; i++) {
      if (word2[i] === undefined) {
        return false;
      }

      if (word1[i] !== word2[i]) {
        setForward(word1[i], word2[i]);
        return true;
      }
    }

    return true;
  };

  // 1. collect all letters & collect the forward/backward relations
  //  a <-->f  f<-->d

  for (let i = 0; i < words.length; i++) {
    for (let char of words[i]) {
      letters.add(char);
    }

    if (i > 0) {
      const isValid = collectForward(words[i - 1], words[i]);
      if (!isValid) {
        return "";
      }
    }
  }

  // 2. look through the forwardMap, and collect the head layer by layer
  // if backwardMap is empty

  const result = [];

  const collect = (letter) => {
    result.push(letter);
    letters.delete(letter);

    if (forwardMap.has(letter)) {
      for (let next of forwardMap.get(letter)) {
        backwardMap.get(next).delete(letter);

        if (backwardMap.get(next).size === 0) {
          backwardMap.delete(next);
        }
      }

      forwardMap.delete(letter);
    }
  };

  while (letters.size > 0) {
    let isHeadFound = false;

    for (let letter of letters) {
      if (!backwardMap.has(letter)) {
        collect(letter);
        isHeadFound = true;
      }
    }

    // circle found
    if (!isHeadFound) {
      return "";
    }
  }

  return result.join("");
};
```
