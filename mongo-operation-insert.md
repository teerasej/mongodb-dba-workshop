
# Insert Operation

## InsertOne

### Workshop ผ่าน Compass
1. Login เข้า Sandbox 
2. เลือก database `video`
3. กดปุ่ม (+) เพื่อเพิ่ม collection ตั้งชื่อว่า `movieScratch`
4. เลือก collection ที่สร้างขึ้นใหม่
5. กดปุ่ม **insert document**
6. กรอกข้อมูล

```bash
"year":"2018","title":"Rocky"}`
```

7. กดปุ่ม **insert**
8. ทดลองกดปุ่มแก้ไขใน collection view

### Workshop ผ่าน Shell
1. Login เข้า Sandbox
2. เลือก database `video`
3. แสดงชื่อ collections ทั้งหมด ด้วย `movieScratch`
4. รันคำสั่ง `insertOne({})` เพื่อเพิ่ม document ใน collection

```js
db.movieScratch.insertOne({title: "Infinity War", year: 2018 })
```

- เราสามารถกำหนด `_id` ได้ถ้าต้องการ

## InsertMany

แบบปกติ ถ้าเกิด error ระหว่างการรัน กระบวนการจะสิ้นสุดที่ document ที่เกิด error

```js
db.<collection>.insertMany([])
```

ถ้าต้องการให้ Mongo ทำการ insert ต่อ แม้ว่าจะเกิด error ก็ตาม ให้เพิ่ม option เข้าไปในคำสั่ง `insertMany()`

```js
db.<collection>.insertMany([], { "ordered":false })
```

- ถ้า `_id` ซ้ำกันจะเกิด Error