
# สร้าง Route 

เปิดไฟล์ `index.js`

เขียนสร้าง route สำหรับ **CRUD** Operation (**C**reate, **R**ead, **U**pdate, **D**elete)

```js
const express = require('express')
const app = express()
const port = 3000
app.use(express.json());

app.get('/', (req, res) => {
    res.send('Hello World!')
})

// read
app.get('/people', async (req,res) => {
    res.json({});
})

// create
app.post('/people', async (req,res) => {
    res.json({});
})

// update
app.put('/people', async (req,res) => {
    res.json({});
})

// delete
app.delete('/people', async (req,res) => {
    res.json({});
})

app.listen(port, () => console.log(`Product API listening on port ${port}!`))
```

บันทึกไฟล์ และทดสอบรัน Web API ด้วย Nodemon

```bash
nodemon index
```
