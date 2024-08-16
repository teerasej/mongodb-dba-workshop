
# Log Rotation

## 0. Setup environment 

ให้แน่ใจว่าได้

1. ทำการรัน MongoDB local server ตามขั้นตอนใน [MongoD Command](../../connect-mongodb-with-shell.md) แล้ว

## 1. เชื่อมต่อ mongoshell กับ MongoDB server

ให้ทำการเปิด mongoshell และรันคำสั่งด้านล่างเพื่อเชื่อมต่อกับ MongoDB server ที่ต้องการตั้งค่า slow query threshold (ในที่นี้คือ local server)

```bash
mongosh 
```

## 2. ใช้คำสั่ง log rotation 

รันคำสั่งด้านล่างเพื่อทำการ rotate log file ของ MongoDB server ที่เปิดอยู่

```javascript
db.adminCommand({logRotate:1})
```

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

## Optional: การตั้งค่า log rotation ใน mongod.conf

```conf
systemLog:
  destination: file
  path: C:\path\to\your\log\mongod.log
  
  logAppend: true
  logRotate: reopen
```