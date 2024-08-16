
# MongoTop 


# Mongostat

## 0. เช็คการทำงานของ MongoDB Database Tools 

ใช้คำสั่งด้านล่างเพื่อเช็คว่า MongoDB Database Tools ทำงานได้ถูกต้องหรือไม่

### Windows 

1. ทดสอบเปิดดูที่ติดตั้ง MongoDB Database Tools ผ่าน File Explorer ที่ `C:\Program Files\MongoDB` ถ้ามีจะเห็นเป็น folder ชื่อ `Tools` และมีโปรแกรม `mongostat.exe` อยู่ภายใน
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

## 3. การใช้งาน mongotop แบบทั่วไป 

รันคำสั่งด้านล่างเพื่อดูข้อมูลของ MongoDB ที่กำลังทำงานอยู่

```bash
mongotop "mongodb+srv://teerasej@cluster0.hkdm2.mongodb.net/"
```
ระบบจะทำการถาม password ของ user ที่เราใช้งาน ให้ใส่ password ของเราลงไป

จะเห็นข้อมูลถูกแสดงออกมาเรื่อยๆ ซึ่งจะเป็น database หรือ collection ที่มีการ actives ล่าสุด ถ้าไม่เห็นข้อมูลออกมา แสดงว่าไม่มีการใช้งานใดๆ ในขณะนั้น

## 4. การกำหนด output ของ mongotop

เรากำหนดรูปแบบการแสดงข้อมูลของ mongostat ได้ด้วยการใช้ flag `--rowcount` และ 
    - `--rowcount` คือ จำนวน row ที่จะแสดงข้อมูล

```
mongostat --rowcount=3 "mongodb+srv://teerasej@cluster0.hkdm2.mongodb.net/" 2
```

