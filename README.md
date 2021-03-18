# @buccaneerai/rxjs-fs
> 💾 RxJS operators and utilities for working with files and file streams locally

## Installation
This is a private package. It requires setting up access in your npm config.

```bash
yarn add @buccaneerai/rxjs-fs
```

## API

### `appendToFile`
Appends a stream of data to a file:
```javascript
import path from 'path';
import {of} from 'rxjs';
import {appendFile} from 'rxfs';

const data = [
  '"animal","coolness"',
  '"dolphin",10',
  '"algea",1',
  '"mermaid",6',
  '"octopus",9',
  '"octopus",9',
  '"narwhale",8',
];

const writeStream$ = of(...data).pipe(
  appendFile({filePath: path.resolve(__dirname, './output.csv')})
);
// write the input observable to the file
writeStream$.subscribe(console.log);
```

### `fromFile`
Streams data from a file as a stream of Buffers.
```js
import path from 'path';
import {fromFile} from '@buccaneerai/rxjs-fs';

const csvContentAsBuffer$ = fromFile({
  filePath: path.resolve(__dirname, './my-csv.csv'),
});
csvContentBuffer$.subscribe(console.log);
// "name","scariness"
// "Blackbeard",10
// "Morgan",9
// "Sparrow",2
// "Crunch",1
```

### shortenChunks
Takes a stream of Buffer objects and ensures that they are shortened to the desired size.  Useful, for example, if you want to control the size of a file upload.
```js
import {shortenChunks} from '@buccaneerai/rxjs-fs';
```

### `writeToFile`
Writes data to file (overwriting any previous contents).
```js
import path from 'path';
import {of} from 'rxjs';
import {writeFile} from '@buccaneerai/rxjs-fs';

const data = [
  '"animal","coolness"',
  '"dolphin",10',
  '"algea",1',
  '"mermaid",6',
  '"octopus",9',
  '"octopus",9',
  '"narwhale",8',
];

const writeStream$ = of(...data).pipe(
  writeFile({filePath: path.resolve(__dirname, './output.csv')})
);
// write the input observable to the file
writeStream$.subscribe(console.log);
```
