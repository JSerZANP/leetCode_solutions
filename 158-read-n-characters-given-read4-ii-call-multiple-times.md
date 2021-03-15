Here is me explaining it on youtube: https://youtu.be/OE-quj_pBeE

```js
/**
 * Definition for read4()
 * 
 * @param {character[]} buf Destination buffer
 * @return {number} The number of characters read
 * read4 = function(buf) {
 *     ...
 * };
 */

/**
 * @param {function} read4()
 * @return {function}
 */
var solution = function(read4) {
    /**
     * @param {character[]} buf Destination buffer
     * @param {number} n Number of characters to read
     * @return {number} The number of actual characters read
     */
    const lastUnread = []
    
    return function(buf, n) {
        // use lastUnread first
      
        while (buf.length < n && lastUnread.length > 0) {
          buf.push(lastUnread.shift())
        }
      
        while (buf.length < n) {
          const bufferFor4 = []
          read4(bufferFor4)
          if (bufferFor4.length === 0) {
            break
          }
          buf.push(...bufferFor4)
        }
      
        // if we read too much
        while (buf.length > n) {
          lastUnread.unshift(buf.pop())
        }
       
        return buf.length
    };
};
```
