
# การเข้าใช้งาน Log ของ MongoDB บนเครื่องเซิฟเวอรของเราเอง

## ที่อยู่ของไฟล์ log (Windows)

```
C:\Program Files\MongoDB\Server\<version>\log
```

## การใช้งาน mongo shell 

> ให้แน่ใจว่าได้สร้าง directory C:/data/db ไว้เพื่อเก็บข้อมูลของ MongoDB ก่อน

1. เปิด Command Prompt และเข้าไปที่โฟลเดอร์ที่ติดตั้ง MongoDB เช่น **C:\Program Files\MongoDB\Server\7.0\bin**
2. พิมพ์คำสั่งดังนี้

```
mongod 
```

3. เปิด command prompt อีกหน้าต่าง เพื่อใช้คำสั่ง mongosh ในการเชื่อมต่อเข้า mongodb server

```
mongosh
```

4. ใช้คำสั่งด้านล่างเพื่อแสดงรายการของ log ทั้งหมด

```
show logs
```

5. ใช้คำสั่งด้านล่างเพื่อแสดง log ประเภท global

```
show log global
```