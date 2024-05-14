```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function (s, numRows) {
  if (numRows === 1) return s;
  const rows = new Array(numRows).fill("");

  let direction = 1;
  let nextRow = 0;
  for (const char of s) {
    // for each char place at nextRow
    rows[nextRow] += char;

    const [newDirection, row] = getNextRow(nextRow, direction);
    nextRow = row;
    direction = newDirection;
  }

  function getNextRow(row, direction) {
    const next = row + direction;
    if (next < 0 || next >= numRows) {
      return [-direction, row - direction];
    } else {
      return [direction, next];
    }
  }

  return rows.join("");
};
```

Another try

```js
/**
 * @param {string} s
 * @param {number} numRows
 * @return {string}
 */
var convert = function (s, numRows) {
  if (s.length === 0) return s;
  if (numRows === 1) return s;

  const rows = new Array(numRows).fill("");
  let currentRow = -1;
  let direction = 1;
  let i = 0;
  while (i < s.length) {
    let nextRow = currentRow + direction;
    if (nextRow >= numRows || nextRow < 0) {
      direction *= -1;
      nextRow = currentRow + direction;
    }
    currentRow = nextRow;
    rows[currentRow] += s[i];
    i += 1;
  }
  return rows.join("");
};
```
