
# Mongo Restore

> ส่วนนี้ต้องทำ mongodump ตามขั้นตอนใน [mongodump](mongodump.md) ก่อน

## 0. เช็คการทำงานของ MongoDB Database Tools 

ใช้คำสั่งด้านล่างเพื่อเช็คว่า MongoDB Database Tools ทำงานได้ถูกต้องหรือไม่

### Windows 

1. ทดสอบเปิดดูที่ติดตั้ง MongoDB Database Tools ผ่าน File Explorer ที่ `C:\Program Files\MongoDB` ถ้ามีจะเห็นเป็น folder ชื่อ `Tools` และมีโปรแกรม `mongodump.exe` อยู่ภายใน
2. ถ้าไม่มีให้ดาวน์โหลด MongoDB Database Tools จาก [เว็บไซต์ของ MongoDB](https://www.mongodb.com/try/download/database-tools) และติดตั้งใหม่

### MacOS

1. เปิด terminal 
2. รันคำสั่งด้านล่าง เพื่อแสดง version ของ MongoDB Database Tools

```bash
mongodump --version
```

3. ถ้าไม่ติดปัญหา จะแสดง version ของ MongoDB Database Tools ออกมา ประมาณด้านล่าง 

```bash
mongodump version: 100.9.5
git version: 90481484c1783826fe26ca18bbdcd30e933f3b88
Go version: go1.21.11
   os: darwin
   arch: arm64
   compiler: gc
```

> ถ้าไม่สามารถรันคำสั่งได้ [ให้ติดตั้ง MongoDB Database Tools ใหม่ผ่าน homebrew ตามขั้นตอนบนเว็บไซต์ของ MongoDB](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/)


## 2. การ Setup environment 

ก่อนทำตามขั้นตอนนี้ ให้แน่ใจว่าได้ทำ
   1. ตามขั้นตอนใน [mongodump](mongodump.md) เรียบร้อยแล้ว
   2. ตามขั้นตอนใน [Run MongoDB with Shell](../../connect-mongodb-with-shell.md) เรียบร้อยแล้ว

#### Windows 

1. ให้เปิดโปรแกรม VS Code และเปิด terminal ขึ้นมา
2. จากด้านบนขวาของ Terminal ให้เลือก New Terminal > Command Prompt
3. รันคำสั่งด้านล่างเพื่อเข้าไปเริ่มการทำงานของ mongodb ใน Program Files ที่ติดตั้ง

```bash 
cd "C:\Program Files\MongoDB\Server\7.0\bin"
```
```bash
mongod --dbpath "C:\data\db"
```

#### MacOS 

1. ให้เปิดโปรแกรม VS Code และเปิด terminal ขึ้นมา
2. รันคำสั่งด้านล่างเริ่มการทำงานของ mongodb 

```bash
brew services start mongodb-community@7.0
```

### 3. เตรียมพร้อมรันคำสั่ง mongorestore

#### Windows

เปิดโปรแกรม Command Prompt และรันคำสั่งด้านล่าง เพื่อเข้าไปที่ directory ที่มีคำสั่ง `mongorestore.exe` อยู่

```bash
cd "C:\Program Files\MongoDB\Tools\100\bin"
```

#### MacOS

สำหรับ MacOS สามารถใช้ terminal เดิมได้เลย

### 3. รันคำสั่ง mongorestore

ใช้คำสั่งด้านล่างเพื่อ dump ข้อมูลจาก cluster ไปยัง folder `dump` ที่เราสร้างไว้

1. ส่วนของ `uri` ให้ใช้ connection string ที่เราคัดลอกมาจาก Atlas และเพิ่ม username และ password ของเราเข้าไป
2. ส่วนของ `db` ระบุเป็นชื่อ database ที่ต้องการ dump ข้อมูลออกมา
3. ส่วนของ `out` ระบุเป็น path ของ folder ที่เราต้องการให้ข้อมูลถูก dump ออกมา

#### Windows

ให้แน่ใจว่า path ของ `--archive` ชี้ไปที่ไฟล์ที่ได้จากขั้นตอน mongodump และเช็คว่ามีไฟล์นั้่นอยู่ใน folder `C:\dump` หรือไม่

```bash
mongorestore --gzip --archive=\dump\backup.gz --drop "mongodb://localhost:27017/"
```

#### MacOS

```bash
mongorestore --gzip --archive=./dump/backup.gz --drop "mongodb://localhost:27017/"
``` 

### 4. ตรวจสอบข้อมูลที่ dump ออกมา  

ให้ใช้ Mongo Compass เชื่อมต่อกับ cluster ที่อยู่ใน local mongodb ของเรา และเลือกดูข้อมูลที่เรา store เข้าไปออกมา

Connection string

```bash
mongodb://localhost:27017/
```