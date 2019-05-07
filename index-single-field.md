# Single Field Indexes

จุดเด่น
- เรียบง่ายที่สุด
- สร้าง keys จาก 1 field เท่านั้น
- สามารถหา
- สามารถใช้ dot notation (`.`) ในการทำ index field จาก document ย่อย (subdocuments) 

```js
db.<collection>.createIndex({ <field>: <direction> })
```

## Workshop

### import ข้อมูล (ถ้ายังไม่ได้ทำ)

[ดูขั้นตอนการ import ข้อมูลได้ที่นี่](mongo-import.md)

### ทดสอบ Single Field Indexes แบบทั่วไป

อย่าลืมคำสั่ง `use nfmongop` นะ

1. รันคำสั่งด้านล่าง เพื่อแสดง document และรายละเอียดการคำนวน

```js
db.people.find({"ssn": "720-38-5636"}).explain("executionStats")
```

สังเกตว่ามีการใช้คำสั่ง `.explain("executionStats")` ด้วย

2. สังเกตค่าต่อไปนี้ จะเห็นว่าอัตราส่วนเยอะมาก
	- **nReturned:1** (จำนวน document ที่ได้กลับมา)
	- **totalDocsExamined** (จำนวน document ที่ไล่หาทั้งหมด)
	- **totalKeysExamined:0** (ไม่มี keys ที่ถูกใช้ค้นหา)
	- **executionTimeMillis** (จำนวนเวลาที่ใช้)

3. รันคำสั่งสร้าง index จาก field ที่ชื่อ **ssn**

```js
db.people.createIndex({ ssn: 1 })
```

4. น่าจะได้ผลลัพธ์ประมาณนี้ 

```json
{
	"createdCollectionAutomatically" : false,
	"numIndexesBefore" : 1,
	"numIndexesAfter" : 2,
	"ok" : 1
}
```

5. รันคำสั่ง `find()` อีกครั้ง
6. สังเกตค่า 
```bash
winningPlan > inputStage > stage: IXSCAN
```
7. สังเกตค่า **executionStats** อีกครั้ง

จากนั้นลองรันคำสั่ง `find()` ใน field อื่น เช่น `.find({ last_name: "Acevedo" })`

และสังเกตค่า **winningPlan** กับ **executionStats**

### ทดสอบ Single Fields Index แบบ sub-document

1. ทดสอบสร้าง collection ใหม่
2. เพิ่ม document แบบมี sub-document ลงไปใน collection จำนวนหนึ่ง
3. ทดสอบใช้คำสั่ง `db.<collection>.createIndex({ field.subfield: 1 }) `
4. ใช้คำสั่ง find แบบตัวอย่างข้างต้นเพื่อทดสอบผลของการทำ index


### การหาข้อมูลแบบ Range ใน Single Field Indexes

1. รันคำสั่ง 

```js
db.people.find({'snn': { $gte: '000-00-0000', $lt: '556-00-0000' }}).explain("executionStats")
```

2. สังเกตค่า **executionStats** ว่าค่า **nReturned** เท่ากับ ค่า **totalKeysExamined** เป็นอัตราส่วน 1:1 ถือว่าดีมาก
3. รันคำสั่งด้านล่างเพื่อหาข้อมูลเป็น set

```js
db.people.find({"ssn": { $in: ["720-38-5636","008-74-2203"]}}).explain("executionStats")
```

และสังเกตค่า **winningPlan** กับ **executionStats** จะเห็นว่าค่า **totalKeysExaminded** มีจำนวนที่มากกว่า **nReturned** ซึ่งถือว่าพอรับได้ 

ส่วนนี้ขึ้นอยู่กับ Algorithm ด้วยครับ