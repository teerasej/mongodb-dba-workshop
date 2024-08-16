
# Monitoring slow queries

## 0. Setup environment 

ให้แน่ใจว่าได้

1. ทำตามขั้นตอนใน [mongodump](../tools/mongodump.md) เรียบร้อยแล้ว
2. ทำตามขั้นตอนใน [mongorestore](../tools/mongorestore.md) เรียบร้อยแล้ว
3. ทำการรัน MongoDB local server ตามขั้นตอนใน [MongoD Command](../../connect-mongodb-with-shell.md) แล้ว


## 1. การตั้งค่า threshold ให้ slowms

1. ให้ทำการเปิด mongoshell และรันคำสั่งด้านล่างเพื่อเชื่อมต่อกับ MongoDB server ที่ต้องการตั้งค่า slow query threshold (ในที่นี้คือ local server)

```bash
mongosh 
```

2. รันคำสั่งด้านล่างเพื่อปิดการทำงานของ Profiler และตั้งค่า threshold เป็น 25ms ทำให้ query ที่ใช้เวลามากกว่า 25ms ถือว่าเป็น slow query และจะถูกบันทึกลงใน log

```javascript
db.setProfilingLevel(0, { slowms:25 })
```

## 2. ทดสอบการทำงานของ slow query

1. ใช้ mongo compass เชื่อมต่อไปที่ local server
2. เลือก `movies` collection และรัน query ตามเงื่อนไขด้านล่าง

filter
```json
{ "genres": "Drama" }
``` 

3. ทดสอบการทำงานเพื่อให้แน่ใจว่า Query ที่เกิดขึ้นใช้เวลามากกว่า 25ms ตามที่กำหนดไว้ใน threshold

## 3. ตรวจสอบการทำงาน

### Windows 

1. โดยปกติ Log จะอยู่ที่ `C:\Program Files\MongoDB\Server\<version>\log\mongod.log` 
2. เปิดโดยใช้เครื่องมือที่ถนัด และหา keyword `SLOW QUERY` ใน log file โดย scroll มาช่วงล่างๆ ที่เป็น log ล่าสุด

### MacOS

1. ในที่นี้ถ้าเราใช้ homebrew ในการติดตั้ง log จะอยู่แตกต่างกัน[ตามระบบ mac ที่ใช้](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) 

 Intel chip: 
```
/usr/local/var/log/mongodb
```
 Apple chip (M)
```
/opt/homebrew/var/log/mongodb
```
2. เปิดไฟล์ log โดยใช้เครื่องมือที่ถนัด และหา keyword `SLOW QUERY` ใน log file โดย scroll มาช่วงล่างๆ ที่เป็น log ล่าสุด