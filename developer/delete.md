
# DELETE

เปิดไฟล์ `index.js` แล้วเขียนใช้ส่วน Route `DELETE /people`

```js
app.delete('/people', async (req,res) => {

    let targetPeople = req.body

    let client = await dbConnection.connect()
    let collection = client.db('nfmongop').collection('people')

    // สร้าง filter object ที่กำหนด ObjectId เป้าหมาย
    let filter = { _id: ObjectId(targetPeople._id) }

    let result = await collection.remove(filter)
    client.close()

    res.json(result);
})
```

ทดสอบการทำงานผ่าน POST Man `DELETE /people` โดยกำหนดค่า JSON ในส่วน Body

```json
{
    "_id": "<ใช้เลข ObjectId ที่ได้ในขั้นตอน insert>"
}
```