
# MongoDump

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

1. ให้แน่ใจว่าได้[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../setup/README.md)
2. ให้ทำการเพิ่ม IP ของเครื่องที่ต้องการเชื่อมต่อ Cluster ตามขั้นตอนใน [Network Security](../security/network.md)
3. ให้ทำการคัดลอก connection string ของ cluster ที่ต้องการใช้งาน จากปุ่ม connect ของ Cluster และเลือก mongo shell
   <img width="640" alt="2024-08-14_23-52-10" src="https://github.com/user-attachments/assets/b0b489e1-983b-478e-8902-ad83cb23c40f">

4. เราจะได้ connection string มาประมาณนี้

```bash
mongosh "mongodb+srv://cluster0.hkdm2.mongodb.net/" --apiVersion 1 --username teerasej
```

## 3. การใช้งาน mongodump

### 1. สร้าง folder สำหรับ dump ข้อมูล

#### Windows 

สร้าง folder ใหม่ ใน `C:\` ชื่อ `dump` โดยคลิกขวาที่ `C:\` > New > Folder และตั้งชื่อว่า `dump`

#### MacOS

เปิด Terminal และสร้าง folder ใหม่ ใน root directory โดยใช้คำสั่งด้านล่าง

```bash
mkdir /dump
```

จากนั้นรันใช้คำสั่งด้านล่าง เพื่อเช็คว่า folder ถูกสร้างขึ้นมาหรือไม่

```bash
ls
```

### 2. เตรียมพร้อมรันคำสั่ง mongodump

#### Windows

เปิดโปรแกรม Command Prompt และรันคำสั่งด้านล่าง เพื่อเข้าไปที่ directory ที่มีคำสั่ง `mongodump.exe` อยู่

```bash
cd "C:\Program Files\MongoDB\Tools\100\bin"
```

#### MacOS

สำหรับ MacOS สามารถใช้ terminal เดิมได้เลย

### 3. รันคำสั่ง mongodump

ใช้คำสั่งด้านล่างเพื่อ dump ข้อมูลจาก cluster ไปยัง folder `dump` ที่เราสร้างไว้

1. ส่วนของ `uri` ให้ใช้ connection string ที่เราคัดลอกมาจาก Atlas และเพิ่ม username และ password ของเราเข้าไป
2. ส่วนของ `db` ระบุเป็นชื่อ database ที่ต้องการ dump ข้อมูลออกมา
3. ส่วนของ `out` ระบุเป็น path ของ folder ที่เราต้องการให้ข้อมูลถูก dump ออกมา

#### Windows

```bash
mongodump --uri="mongodb+srv://cluster0.hkdm2.mongodb.net/" --username=<username> --password=<password> --db=sample_mflix --out=/dump
```

#### MacOS

```bash
mongodump --uri="mongodb+srv://cluster0.hkdm2.mongodb.net/" --username=<username> --password=<password> --db=sample_mflix --out=./dump
``` 

### 4. ตรวจสอบข้อมูลที่ dump ออกมา  

#### Windows

ให้เปิดเช็คข้อมูลที่ folder `C:\dump` ที่เราสร้างไว้ จะเห็นไฟล์ bson และ metadata ของ database ที่เรา dump ออกมา

#### MacOS  

ใช้คำสั่งด้านล่างในการเช็คข้อมูลที่ folder `/dump` ที่เราสร้างไว้

```bash
ls dump/sample_mflix
```

### Optional (1) การ dump ข้อมูลแบบ compress ไฟล์ 

ใช้คำสั่งด้านล่างเพื่อ dump ข้อมูลและบีบอัดไฟล์เป็น .tar หรือ .zip

> อย่าลืมเปลื่ยน `uri`, `username`, `password` ให้ตรงกับ cluster ของเรา

#### Windows

```bash
mongodump --uri="mongodb+srv://cluster0.hkdm2.mongodb.net/" --username=<username> --password=<password> --db=sample_mflix --gzip --archive=\dump\backup.gz
```

#### MacOS

```bash
mongodump --uri="mongodb+srv://cluster0.hkdm2.mongodb.net/" --username=<username> --password=<password> --db=sample_mflix --gzip --archive=./dump/backup.gz
```
