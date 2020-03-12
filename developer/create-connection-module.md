
# สร้าง Connection Module ไว้ใช้

1. สร้างไฟล์ `db.js`
2. เขียนใช้งาน MongoDB client

```js
const MongoClient = require('mongodb').MongoClient;
const url = 'mongodb://localhost:27017';
const dbName = 'nfmongop';

const client = new MongoClient(url);

module.exports = client;
```