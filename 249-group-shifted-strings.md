Here is me explaining it on youtube: https://youtu.be/7dbJCbWGwnc
```js
/**
 * @param {string[]} strings
 * @return {string[][]}
 */

// Time: O(all letters)
// Space: worst O(strings length)
var groupStrings = function(strings) {
    // a b d  => a (1) b (2) d => b (1) c (2) e => 12 => 1_2
    // a (25) z => b (-1) a 25  => 25_1
    // a  => OK => ''
    const LENGTH_ALL_LETTERS = 26
    // create a string joined by distances between letters
    const getHash = (str) => {
      if (!str.length) return 'empty';
      if (str.length === 1) return ''
      const distances = []
      for (let i = 1; i < str.length; i++) {
        const distance = (str.charCodeAt(i) - str.charCodeAt(i - 1) + LENGTH_ALL_LETTERS) % LENGTH_ALL_LETTERS
        distances.push(distance)
      }
      
      return distances.join('')
    }
    
    // Map<hash, string[]>
    const resultMap = new Map()
    
    for (let string of strings) {
      const hash = getHash(string)
      let group = resultMap.get(hash)
      
      if (!group) {
        group = []
        resultMap.set(hash, group)
      }
      
      group.push(string)
    }
  
    return [...resultMap.values()]
};
```
