# torrent-file [![npm](https://img.shields.io/npm/v/@ctrl/torrent-file.svg?maxAge=3600)](https://www.npmjs.com/package/@ctrl/torrent-file) [![CircleCI](https://circleci.com/gh/TypeCtrl/torrent-file.svg?style=svg)](https://circleci.com/gh/TypeCtrl/torrent-file) [![coverage status](https://codecov.io/gh/typectrl/torrent-file/branch/master/graph/badge.svg)](https://codecov.io/gh/typectrl/torrent-file)

> Parse a torrent file and read encoded data. 

This project is based on [parse-torrent](https://www.npmjs.com/package/parse-torrent) and [node-bencode](https://github.com/themasch/node-bencode) to parse the data of a torrent file. This library implements its own [bencode](http://www.bittorrent.org/beps/bep_0003.html) encoder and decoder and keeps dependencies to a minimum.

### Install
```console
npm install @ctrl/torrent-file
```

### API

##### info
The content of the metainfo file.
```ts
import fs from 'fs';
import { info } from '@ctrl/torrent-file';

const torrentInfo = info(fs.readFileSync('myfile'));
console.log({ torrentInfo });
```

##### files
data about the files described in the torrent file, includes hashes of the pieces
```ts
import fs from 'fs';
import { files } from '@ctrl/torrent-file';

const torrentFiles = files(fs.readFileSync('myfile'));
console.log({ torrentFiles });
```

##### hash
sha1 of torrent file info. This hash is commenly used by torrent clients as the ID of the torrent. It is async and sha1 encoding is handled by [crypto-hash](https://github.com/sindresorhus/crypto-hash)
```ts
import fs from 'fs';
import { hash } from '@ctrl/torrent-file';

(async () => {
  const torrentHash = await hash(fs.readFileSync('myfile'));
  console.log({ torrentHash });
})()
```

### encode
Use the built in bencode encoder
```ts
import fs from 'fs';
import { encode } from '@ctrl/torrent-file';

encode({ name: 'my string to encode' });
```

### decode
Easily get the raw data inside a torrent file.
```ts
import fs from 'fs';
import { decode } from '@ctrl/torrent-file';

decode(fs.readFileSync('myfile'));
```

### See Also
[parse-torrent](https://www.npmjs.com/package/parse-torrent) - "@ctrl/torrent-file" torrent parsing based very heavily off this project  
[node-bencode](https://github.com/themasch/node-bencode) - bencoder built into this project heavily based off this project   
