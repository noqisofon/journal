---
title: VFile について
draft: false
date: 2022-12-04T17:25:50+09:00
categories:
  - Development
  - NodeJS
---

`to-vfile` は `VFile` を扱うモジュールです。

``` js
import { read, write, toVFile } from 'to-vfile';
```

`remark` と相性がいいっていうか、同じ作者さんが作ってるみたいなので、`remark` の例によく出てきます。

`read()` は実のところ、Perl における `slurp` のようなものです。  
違うのは `string` ではなくて `VFile` を返すところです。

``` js
const vfile /* : VFile */ = await read( './hoge.md' );
```

`.value` でファイルの内容を参照できます。

``` js
console.log( vfile.value );   // => <ファイルの内容>
```

`write()` がほんとにわかりませんでしたが、`test.js` を見て理解することができました:

``` js
const destFilePath = changeExtention( './hoge.md', '.html' );
await write( { path: destFilePath, data: 'Hello, World!' } );
```

NodeJS の `fs.writeFile()` 風に書くと以下のようになります:

``` js
async function writeVFile(filepath, data/*, options */) {
    const vfile = {
        path: filepath,
        data: data
    };

    await write( vfile );
}
```
