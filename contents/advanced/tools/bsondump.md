
# BSONDUMP


## 0. Setup environment 

ให้แน่ใจว่าได้

1. ทำตามขั้นตอนใน [mongodump](../tools/mongodump.md) เรียบร้อยแล้ว

## 1. เตรียมพร้อมรันคำสั่ง bsondump


#### Windows

1. เปิดโปรแกรม Command Prompt และรันคำสั่งด้านล่าง เพื่อเข้าไปที่ directory ที่มีคำสั่ง `mongofiles.exe` อยู่

```bash
cd "C:\Program Files\MongoDB\Tools\100\bin"
```

#### MacOS

1. สำหรับ MacOS สามารถนำไฟล์รูปภาพมาไว้ใน folder และเปิด terminal ขึ้นมาที่ folder นั้น เพื่อให้สามารถอ้างอิงชื่อไฟล์ได้โดยตรง 

### 2. รันคำสั่ง bsondump

ใช้คำสั่งด้านล่างเพื่อใช้ bsondump แสดงข้อมูลจาก BSON file ที่เราต้องการดู

#### Windows

```bash
bsondump --pretty \dump\sample_mflix\users.bson
```

```bash
bsondump --pretty --type=debug \dump\sample_mflix\users.bson
```

#### MacOS

แบบ --pretty จะแสดงข้อมูลใน BSON file ในรูปแบบที่อ่านง่าย

```bash
bsondump --pretty ~/dump/sample_mflix/users.bson
```

สำหรับแบบ `--type=debug` จะแสดงข้อมูลทั้งหมดใน BSON file และแสดงข้อมูลที่เป็น binary ด้วย เช่น data type และ size ของข้อมูลเป็นหน่วย byte

```bash
bsondump --pretty --type=debug \dump\sample_mflix\users.bson
```