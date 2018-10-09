# Sorting with indexes

มี 2 แบบ
- In memory
- ใช้ index

## In memory 

- เวลา Sort ปกติ (In-memory) จะมีการโหลด document จาก disk เข้า RAM
- แบบใช้ index จะเร็วกว่า แต่จะ sort ตาม key ที่ถูกใช้ทำ indexes เท่านั้น 

## Workshop 

### import ข้อมูล (ถ้ายังไม่ได้ทำ)

1. เปิด Command Prompt หรือ Terminal มาที่โฟลเดอร​์ **B-Performance**
2. รันคำสั่ง 

```bash
mongoimport --db nfmongop --collection people --file people.json
```

### ทดสอบการ sort

อย่าลืมคำสั่ง `use nfmongop` นะ

1. รันคำสั่งด้านล่าง และสังเกตว่ามีการใช้ `.sort({})` ที่เรียกใช้ index ของเรา

```js
db.people.find({}, { _id : 0, last_name: 1, first_name: 1, ssn: 1 }).sort({ ssn: 1 })
```

2. รันคำสั่งด้านล่าง เพื่อดูข้อมูลการทำงานล่าสุดบน Collection 

```js
var exp = db.people.explain('executionStats')

exp.find({}, { _id : 0, last_name: 1, first_name: 1, ssn: 1 }).sort({ ssn: 1 })
```

3. สังเกตค่า **winningPlan** กับ **executionStats** จะเห็นว่า **totalKeysExamined** มีการใช้งาน และสังเกตเวลาท่ี่ใช้
4. รันคำสั่งใหม่ โดยใช้ field อื่นที่ไม่ได้ทำ index แทน

```js
exp.find({}, { _id : 0, last_name: 1, first_name: 1, ssn: 1 }).sort({ first_name: 1 })
```

5. สังเกตค่า **winningPlan** กับ **executionStats** ในส่วนของ **executionTimeMillis** และ **totalKeysExamined** 
6. ทดลองรันคำสั่ง sort แบบ Descending

```js
exp.find({}, { _id : 0, last_name: 1, first_name: 1, ssn: 1 }).sort({ ssn: -1 })
```

7. สังเกตค่า **winningPlan** กับ **executionStats** ในส่วนของ **executionTimeMillis** และ **totalKeysExamined**

### ทดสอบการทำงาน Indexes แบบ Descending

1. รันคำสั่งด้านล่างเพื่อ drop index ทิ้ง

```js
db.people.dropIndexes()
```

2. สร้าง index ด้วย field **ssn** เดิม แต่คราวนี้เป็นแบบ Descending (ค่าเป็น -1)

```js
db.people.createIndex({ ssn: -1 })
```

3. ทดสอบรันคำสั่งด้านล่างอีกครั้ง 

```js
exp.find( { ssn : /^555/ }, { _id : 0, last_name: 1, first_name: 1, ssn: 1 } ).sort( { ssn : -1 } )
```

สังเกตค่า **direction** ใน **winningPlan**
