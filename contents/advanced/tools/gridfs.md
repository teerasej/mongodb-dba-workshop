
# GridFS 


## 0. Setup environment 

ให้แน่ใจว่าได้

1. ทำตามขั้นตอนใน [mongodump](../tools/mongodump.md) เรียบร้อยแล้ว
2. ทำตามขั้นตอนใน [mongorestore](../tools/mongorestore.md) เรียบร้อยแล้ว
3. ทำการรัน MongoDB local server ตามขั้นตอนใน [MongoD Command](../../connect-mongodb-with-shell.md) แล้ว

## 2. เตรียมพร้อมรันคำสั่ง mongofiles

1. ให้ทำการดาวน์โหลดไฟล์รูปภาพ [mongodb.png](mongodb.png) มาไว้ใน directory ที่เหมาะสมตามเครื่องที่เราใช้ด้านล่างนี้

#### Windows

> ดาวน์โหลดไฟล์รูป มาไว้ที่ที่มี `mongofiles.exe` อยู่ เช่น `C:\Program Files\MongoDB\Tools\100\bin`

2. เปิดโปรแกรม Command Prompt และรันคำสั่งด้านล่าง เพื่อเข้าไปที่ directory ที่มีคำสั่ง `mongofiles.exe` อยู่

```bash
cd "C:\Program Files\MongoDB\Tools\100\bin"
```

#### MacOS

1. สำหรับ MacOS สามารถนำไฟล์รูปภาพมาไว้ใน folder และเปิด terminal ขึ้นมาที่ folder นั้น เพื่อให้สามารถอ้างอิงชื่อไฟล์ได้โดยตรง 

### 3. รันคำสั่ง mongofiles

ใช้คำสั่งด้านล่างเพื่อ upload ไฟล์รูปภาพ mongodb.png ขึ้นไปบน MongoDB โดยใช้ชื่อ `mongodb.png`
- `--db` คือ ชื่อ database ที่เราต้องการเก็บไฟล์

```bash
mongofiles put mongodb.png "mongodb://localhost:27017" --db myFiles
```

### 4. ตรวจสอบข้อมูลที่ upload ขึ้นไป

รันคำสั่งด้านล่างเพื่อดูข้อมูลที่ upload ขึ้นไปบน MongoDB

```bash
mongofiles list "mongodb://localhost:27017" --db myFiles
```

### 5. ดึงไฟล์ออกมาจาก MongoDB

ใช้คำสั่งด้านล่างเพื่อดึงไฟล์ mongodb.png ออกมาจาก MongoDB และเก็บไว้ใน directory ที่เราต้องการ

```bash
mongofiles get mongodb.png  "mongodb://localhost:27017"
 --db myFiles --local downloaded.png
```

### 6. Optional ดูรูปแบบของ GridFS ผ่าน Mongo Compass

1. ให้ใช้ Mongo Compass เชื่อมต่อกับ cluster ที่อยู่ใน local mongodb ของเรา และเลือกดูข้อมูลที่เรา upload ขึ้นไป

Connection string

```bash
mongodb://localhost:27017/
```

2. เลือกดู database 'myFiles' และ collection 'fs.files' และ 'fs.chunks'

