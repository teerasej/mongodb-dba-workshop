
# CREATE

เปิดไฟล์ `index.js` แล้วเขียนใช้ส่วน Route `POST /people`

```js
app.post('/people', async (req,res) => {

    // ดึง json มาจาก Request
    let newPeople = req.body

    let client = await dbConnection.connect()
    let collection = client.db('nfmongop').collection('people')

    // insert object ลง database
    let result = await collection.insertOne(newPeople);
    client.close()

    // คืนผลลัพธ์ให้ client
    res.json(result)
})
```

ทดสอบการทำงานผ่าน POST Man `POST /people`  โดยกำหนดค่า JSON ในส่วน Body

```json
{
	"first_name": "John",
	"last_name": "Constantine"
}
```