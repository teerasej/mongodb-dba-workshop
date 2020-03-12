
# READ

เปิดไฟล์ `index.js` แล้วเขียนใช้ส่วน Route `GET /people`

```js
app.get('/people', async (req,res) => {

    // เชื่อมต่อ database
    let client = await dbConnection.connect()
    // เรียกใช้ people collection จาก nfmongop database
    let collection = client.db('nfmongop').collection('people')

    // เรียกใช้ข้อมูลแค่ 10 document
    let result = await collection.find().limit(10).toArray()
    // ปิดการเชื่อมต่อ
    client.close()

    // คืนค่ากลับไปให้ client 
    res.json(result)
})
```

ทดสอบการทำงานผ่าน POST Man `GET /people`