Here is my video explaining it: https://youtu.be/uHEvS8VO0o4


```js
/**
 * Definition for isBadVersion()
 * 
 * @param {integer} version number
 * @return {boolean} whether the version is bad
 * isBadVersion = function(version) {
 *     ...
 * };
 */

/**
 * @param {function} isBadVersion()
 * @return {function}
 */
var solution = function(isBadVersion) {
    /**
     * @param {integer} n Total versions
     * @return {integer} The first bad version
     */
    return function(n) {
        let i = 1;
        let j = n;
        while (i <= j) {
          const middle = Math.floor((i + j) / 2)
          if (isBadVersion(middle)) {
            j = middle - 1
          } else {
            i = middle + 1
          }
        }
        return i
    };
};
```
