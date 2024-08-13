
# Read Operation

1. ให้ใช้ Mongo Compass เชื่อมต่อไปที่ `cluster0-shard-00-00-jxeqq.mongodb.net` ([ดูการตั้งค่าเชื่อมต่อได้ที่นี่](compass-connect-example-cluster.md))
2. เลือก Database **Video** และ collection **Movie**

## find()

```js
.find({ year: 2009 })
```

หรือถ้าต้องการจัดผลลัพธ์ในดูอ่านง่ายใน Shell ก็สามารถใช้ `.pretty()` ตามหลังคำสั่ง `find()` ได้

```js
.find().pretty()
```

### AND Operator

```js
.find({ year: 2009, mpaaRating: "PG-13" })
```


### COUNT Operator

ใช้ในการนับจำนวน collection จากผลลัพธ์

```js
.find().count()
```

### การ filter โดยอิงจาก nested document

ให้สังเกตว่าต้องมี `" "` กำกับ

```js
.find({ "wind.direction.angle": 290 })
```

### Array 

หาค่าตัวใดตัวหนึ่งใน Array ที่ตรงกัน (cast มี type เป็น Array)

```js
.find({ cast: "Robert Downy JR." })
```

หา document แบบที่ค่า Array ตรงเป๊ะๆ 

```js
.find({ cast: ["Robert Downy JR.", "Chris Evan"] })
```

หา document แบบที่เจาะจงตำแหน่งใน Array เช่นในที่นี้จะคืนค่าเป็น document ที่มี "Robert Downy JR." เป็นค่าแรกใน Array เท่านั้น 

```js
.find({ "cast.0": "Robert Downy JR." })
```

### Cursor

- Cursor เป็นตัวชี้ที่ MongoDB ส่งกลับมาให้ Client จากการรันคำสั่ง `find()` (ในที่นี้ Client คือ Mongo Shell) 
- ปกติ Mongo shell จะโหลด 20 document แรกที่ได้จากคำสั่ง `find()`
- เราสามารถรันคำสั่งด้านล่าง เพื่อให้ mongo shell โหลดอีก 20 document ถัดไปมาได้

```bash
it
```

### Projection

- Projection เหมือนเป็นการเลือกให้ Mongo คืนเฉพาะ key ที่เราสนใจใน document ตัวนั้น
- เช่น ถ้าต้องการเฉพาะ `title` key

```js
.find({}, { title: 1 })
```

- และถ้าไม่ต้องการ `_id` key

```js
.find({}, { title: 1, _id: 0 })
```

## ดูเพิ่มเติม

- ดูองค์ประกอบของการ Query ต่างๆ [ได้ที่นี่](https://docs.mongodb.com/manual/reference/operator/query/)

