
# UPDATE

เปิดไฟล์ `index.js` แล้วเขียนใช้ส่วน Route `PUT /people`

```js
app.put('/people', async (req,res) => {


    let targetPeople = req.body

    let client = await dbConnection.connect()
    let collection = client.db('nfmongop').collection('people')

    // สร้าง filter object ที่กำหนด ObjectId ของ document เป้าหมาย
    let filter = { _id: ObjectId(targetPeople._id) }
    // สร้าง query object ที่กำหนดค่าเงื่อนไขอัพเดต
    let query = {
        $set: { first_name: targetPeople.first_name }
    }

    let result = await collection.updateOne(filter, query)
    client.close()

    res.json(result);
})
```

ทดสอบการทำงานผ่าน POST Man `PUT /people` โดยกำหนดค่า JSON ในส่วน Body

```json
{
    "_id": "<ใช้เลข ObjectId ที่ได้ในขั้นตอน insert>",
	"first_name":"Peter"
}
```