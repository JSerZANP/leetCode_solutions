## 1.

Here is a video explaining: https://youtu.be/xoeMhTvg11M

```js
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
var fullJustify = function (words, maxWidth) {
  const result = [];
  let chunk = [];
  let chunkLength = 0;

  const generateSpaces = (n) => {
    if (n === 0) return "";
    return Array(n).fill(" ").join("");
  };

  const flush = (isLast) => {
    // transform chunk into a string
    let spaces = Array(chunk.length).fill("");
    if (isLast) {
      for (let i = 0; i < spaces.length; i++) {
        if (i < spaces.length - 1) {
          spaces[i] = " ";
        } else {
          const rest = maxWidth - chunkLength - i;
          spaces[i] = generateSpaces(rest);
        }
      }
    } else {
      // last space should be empty
      if (spaces.length === 1) {
        spaces[0] = generateSpaces(maxWidth - chunkLength);
      } else {
        const base = Math.floor((maxWidth - chunkLength) / (spaces.length - 1));
        const rest = maxWidth - chunkLength - base * (spaces.length - 1);
        for (let i = 0; i < spaces.length - 1; i++) {
          if (i < rest) {
            spaces[i] = generateSpaces(base + 1);
          } else {
            spaces[i] = generateSpaces(base);
          }
        }
      }
    }

    // genrate the string
    result.push(chunk.map((word, i) => word + spaces[i]).join(""));

    chunk = [];
    chunkLength = 0;
  };

  for (let i = 0; i < words.length + 1; i++) {
    const word = words[i];
    // whether word could be put into the chunk
    if (i === words.length) {
      flush(true /* last chunk */);
    } else if (chunkLength + word.length + chunk.length <= maxWidth) {
      chunk.push(word);
      chunkLength += word.length;
    } else {
      flush();
      i -= 1;
    }
  }

  return result;
};
```

## 2

```js
var fullJustify = function (words, maxWidth) {
  // use a buffer
  // keep adding words until it exeeds maxWidth
  // justify it , collect as result

  const result = [];
  let buffer = [];
  let wordWidthInBuffer = 0;
  for (const word of words) {
    if (wordWidthInBuffer + word.length + buffer.length <= maxWidth) {
      buffer.push(word);
      wordWidthInBuffer += word.length;
    } else {
      // if unable to push then flush
      result.push(buffer);
      buffer = [word];
      wordWidthInBuffer = word.length;
    }
  }
  result.push(buffer);

  return result.map((buffer, i) => {
    if (i !== result.length - 1) {
      // add space to the words except last one
      const wordWidth = buffer.reduce(
        (result, word) => result + word.length,
        0
      );
      let spacesNeeded = maxWidth - wordWidth;
      let index = 0;
      while (spacesNeeded > 0) {
        buffer[index] += " ";
        spacesNeeded -= 1;
        index = (index + 1) % (buffer.length > 1 ? buffer.length - 1 : 1);
      }
      return buffer.join("");
    } else {
      return buffer.join(" ").padEnd(maxWidth, " ");
    }
  });
};
```

Another try

```js
/**
 * @param {string[]} words
 * @param {number} maxWidth
 * @return {string[]}
 */
var fullJustify = function (words, maxWidth) {
  const rows = []; // 2d array of string
  let buffer = [];
  let currentLength = 0;
  for (const word of words) {
    if (buffer.length + currentLength + word.length > maxWidth) {
      rows.push(buffer);
      buffer = [word];
      currentLength = word.length;
    } else {
      buffer.push(word);
      currentLength += word.length;
    }
  }
  if (buffer.length > 0) {
    rows.push(buffer);
  }
  return rows.map((row, i) => {
    if (i === rows.length - 1 || row.length === 1) {
      return row.join(" ").padEnd(maxWidth, " ");
    }
    const totalLength = row.reduce((a, b) => a + b.length, 0);
    const totalSpaceCount = maxWidth - totalLength;
    const baseSpaceCount = Math.floor(totalSpaceCount / (row.length - 1));
    const restSpaceCount = totalSpaceCount % (row.length - 1);
    for (let i = 0; i < row.length - 1; i++) {
      row[i] += " ".repeat(baseSpaceCount + (i < restSpaceCount ? 1 : 0));
    }
    return row.join("");
  });
};
```
