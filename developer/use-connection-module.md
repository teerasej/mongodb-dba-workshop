
# ใช้งาน Connection Module ใน Route

1. เปิดไฟล์ `index.js`
2. เรียกใช้งาน db module 

```js
const express = require('express')
const app = express()
const port = 3000
app.use(express.json());

// เรียกใช้งาน object ID
const {ObjectId} = require('mongodb');

// import mongodb client จาก module
const dbConnection = require('./db');
// กำหนดชื่อฐานข้อมูล
const dbName = 'nfmongop';
```


