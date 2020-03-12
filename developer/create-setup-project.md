
# สร้างโปรเจค 

1. สร้างโฟลเดอร์ `people_api`
2. รันคำสั่งสร้างไฟล์ `package.json` โดยระบุข้อมูลตามสมควร เช่น ชื่อ package, ชื่อเจ้าของ

```bash
npm init
```

3. รันคำสั่งติดตั้ง **Express** module

```bash
npm i express
```

4. สร้างไฟล์ `index.js` ในโฟลเดอร์ของโปรเจค
5. เขียนโค้ดสร้าง Route และการทำงานของ Web API และบันทึกไฟล์

```js
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
    res.send('Hello World!')
})

app.listen(port, () => console.log(`Product API listening on port ${port}!`))
```

6. รันคำสั่งติดตั้ง package ชื่อ `nodemon`

```bash
npm i -g nodemon
```

7. ใช้คำสั่ง nodemon เพื่อรันทดสอบ Web API

```bash
nodemon index
```


