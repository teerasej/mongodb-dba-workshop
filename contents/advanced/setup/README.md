
# สมัคร และสร้าง Cluster บน Mongo Atlas

## 1. สร้าง Atlas Cluster

- สร้าง Account [https://cloud.mongodb.com/links/registerForAtlas](https://cloud.mongodb.com/links/registerForAtlas)
- ลงชื่อเข้าใช้งาน [https://cloud.mongodb.com/user/login](https://cloud.mongodb.com/user/login)

ในขั้นตอนอาจจะมีการให้สร้าง organization ใหม่ หรือใช้ organization ที่มีอยู่แล้วก็ได้

### 2. สร้างโปรเจค 

1. เราสามารถแยกจัดการ Cluster ต่างๆ ได้ด้วยการสร้าง Project ใหม่ โดยเราสามารถกด New Project
<img width="1006" alt="2024-08-14_22-59-09" src="https://github.com/user-attachments/assets/e59a7a7b-aa0f-48e6-a03b-07bdfaae7d6d">

2. ตั้งชื่อ Project ใหม่เป็น `AdvMongoDB` และกด Next 
<img width="1006" alt="2024-08-14_22-59-54" src="https://github.com/user-attachments/assets/c95e3ac8-51b7-43c0-804c-1559e8cabfe3">

3. เช็คให้แน่ใจว่า account ของเราเป็น project owner และกด Create Project
<img width="904" alt="2024-08-14_23-00-38" src="https://github.com/user-attachments/assets/338e4629-90d6-4d4c-871a-a3fe00fdc467">

เราจะได้โปรเจค `AdvMongoDB` ใหม่มาใช้งาน ให้กดเลือกชื่อโปรเจคเพื่อเข้าไปใช้งาน

### 3. สร้าง Cluster

1. จากหน้าโปรเจคเราจะทำการสร้าง Cluster ใหม่ 
<img width="916" alt="2024-08-14_23-01-47" src="https://github.com/user-attachments/assets/94e538e8-20a9-4dae-a88b-59ba47cf830f">

2. กำหนดรายละเอียดของ Cluster ตามนี้
   1. เลือก M0 (Free) เป็น Cluster Tier ของเรา
   2. เลือก Configuration เป็น Cloud Provider ไหนก็ได้ เช่น Azure และเลือก Region ที่ใกล้ที่สุด
   3. เลือก **Automate Security Setup** และ **Preload Sample Data Set**
<img width="1173" alt="2024-08-14_14-30-08" src="https://github.com/user-attachments/assets/b16123c3-03ba-4c19-8d4a-1038adeaa948">



### 4. ตั้งค่า Security ให้ Cluster

1. กำหนด Authentication Method
   1. เลือก Authentication method เป็น Username and Password
   2. กรอก Username c และ Password ตามที่ต้องการ ให้จด Username และ Password นี้ไว้ด้วย
   3. กด Create user
   4. เช็คให้แน่ใจว่ามี Username ของเราอยู่ในรายการ
   <img width="946" alt="2024-08-14_14-37-29" src="https://github.com/user-attachments/assets/82112386-35cd-4938-83a6-f9969fb59110">

2. ในส่วน Where would you like to connect from? 
   1. เลือก My Local Environment 
   2. กด Add My Current IP Address 
   3. กดปุ่ม Add Entry
   4. เช็คให้แน่ใจว่ามี IP ของเราอยู่ในรายการ
   5. กรอก IP: 0.0.0.0 เพิ่มเข้าไปในรายการ ส่วนนี้จะทำให้เราสามารถเชื่อมต่อจากทุกที่ได้
   <img width="855" alt="2024-08-14_14-37-38" src="https://github.com/user-attachments/assets/50986a1c-e6b9-4963-9d01-1a875ce8d8b2">


> **ในที่นี้เราเพิ่ม IP 0.0.0.0 ในการอบรมเท่านั้น นะ นะ นะ**


## 5. เชื่อมต่อไปที่ Cluster ผ่าน MongoDB Compass

1. จากหน้าโปรเจค ให้เลือก Deployment > Database> Cluster0 และกดปุ่ม Connect
<img width="640" alt="2024-08-14_23-52-10" src="https://github.com/user-attachments/assets/b0b489e1-983b-478e-8902-ad83cb23c40f">

2. เลือก **Connect with Mongo Comppass**
<img width="787" alt="2024-08-14_23-53-34" src="https://github.com/user-attachments/assets/f1390f9a-edee-4dc7-a0f7-12dad7eed32c">

3. ยืนยันว่าได้ทำการติดตั้ง MongoDB Compass แล้ว > เลือก version > กด Copy Connection String
<img width="784" alt="2024-08-14_23-54-14" src="https://github.com/user-attachments/assets/13359a1f-d7e5-464f-9906-dcd8c068afcb">

4. เปิดโปรแกรม MongoDB Compass
   1. กดปุ่ม New Connection
   2. วาง connection string และแก้ส่วนของ **<username>** และ **<password>** เป็นค่าที่ตั้งไว้ก่อนหน้านี้
   3. กดปุ่ม Connect
   4. ถ้าการเชื่อมต่อสมบูรณ์จะถูกบันทึกไว้ในรายการ Connection ของเรา
<img width="1263" alt="2024-08-14_23-55-49" src="https://github.com/user-attachments/assets/291e673c-1127-43b4-a740-a352ef8815b0">


## 6. (Optional) เชื่อมต่อไปที่ Cluster ผ่าน Mongo Shell

1. จากหน้าโปรเจค ให้เลือก Deployment > Database> Cluster0 และกดปุ่ม Connect
<img width="640" alt="2024-08-14_23-52-10" src="https://github.com/user-attachments/assets/b0b489e1-983b-478e-8902-ad83cb23c40f">

2. เลือก **Connect with Mongo Shell**
3. ให้แน่ใจว่าได้ทำการติดตั้ง MongoDB Shell บน computer ของเราเรียบร้อยแล้ว
4. กด Copy Connection String (ตัวอย่างจะคล้ายข้อความด้านล่าง)

```
mongosh "mongodb+srv://cluster0.ljb4t.mongodb.net/" --apiVersion 1 --username <username>
```

5. กลับมาที่ Command Prompt ในเครื่องเรา และรันคำสั่งดังกล่าว โดยแทน `<username>` ด้วย username ที่เราสร้างไว้ก่อนหน้านี้
6. ระบบจะแสดงข้อความให้กรอก password ของเรา ให้กรอก password ที่เราสร้างไว้ก่อนหน้านี้
7. ถ้าการเชื่อมต่อสมบูรณ์ ให้ทดสอบการใช้งานด้วยคำสั่ง `show dbs` หรือ `db.help()`
