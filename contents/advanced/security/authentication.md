
# Authentication 


## 1. เปิดไฟล์ mongod.conf

1. เปิดไฟล์ mongod.conf

### Windows 

เปิดไฟล์ `C:\Program Files\MongoDB\Server\7.0\bin\mongod.cfg` ด้วย Editor ที่ถนัด

### MacOS 

ในที่นี้ถ้าเราใช้ homebrew ในการติดตั้ง log จะอยู่แตกต่างกัน[ตามระบบ mac ที่ใช้](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) 

Intel chip: 
```
/usr/local/etc/mongod.conf
```
Apple chip (M)
```
/opt/homebrew/etc/mongod.conf
```

2. เพิ่มส่วนนี้เข้าไปในไฟล์ configuration

```bash
security:
    authorization: enabled
```

ส่วนนี้สามารถทำได้โดย[ใช้คำสั่งผ่านการรัน mongod ได้เช่นเดียวกัน](../../security-localhost-exception.md)

```bash
mongod --auth
```


## 2. ทำการ restart mongod

ทำการปิดและเปิดการทำงานของ MongoDB ใหม่

## 3. เริ่มสร้าง admin account

1. ให้แน่ใจว่าเราได้ทำ[การรัน mongod instance แล้วตามขั้นตอนนี้](../../compass-connect-localhost-cluster.md)

2. ใช้ mongo shell เพื่อเชื่อมต่อกับ mongod instance

```bash
mongosh localhost:27017
```

3. สลับใช้งาน admin database โดยรันคำสั่งด้านล่าง

```bash 
use admin
```

4. ใช้ createUser() method โดยกำหนด username เป็น `globalUserAdmin`, password เป็น `passwordPrompt()`, และ role เป็น `userAdminAnyDatabase`:

```bash
db.createUser(
    {
        user: "globalUserAdmin",
        pwd: passwordPrompt(),
        roles: [
            { role: "userAdminAnyDatabase", db: "admin" }
        ]
    }
)
```

5. กรอกตั้งรหัสผ่านของ `globalUserAdmin` เมื่อมีการถาม 
6. เสร็จแล้วออกจาก mongo shell ด้วยการใช้คำสั่ง quit() หรือ ctrl + C

```bash
quit()
```

## 4. เช็คการเข้าใช้งานแบบไม่ login 

1. อย่างแรกเราจะลองรันใช้งาน mongosh แบบไม่ใช้ admin account

```bash
mongosh localhost:27017
```
2. ทดสอบเข้าใช้งาน sample_mflix database โดยใช้คำสั่งด้านล่าง

```bash
use sample_mflix
```
```bash
db.movies.find()
```

3. จะเห็นว่าเราไม่สามารถใช้งานได้

## 5. เช็คการเข้าใช้งานด้วย username และ password

1. เข้าใช้งาน mongo shell ด้วยการใช้ username และ password ที่เราสร้างไว้

```bash
mongosh -u globalUserAdmin -p --authenticationDatabase admin localhost:27017
```

2. ถ้าเราสามารถเข้าใช้งานได้ แสดงว่าการตั้งค่าการเข้าใช้งานด้วย username และ password สำเร็จ
3. ลองเข้าดูข้อมูลจะสามารถดูได้ตามสิทธิ์ของเรา

```bash
use sample_mflix
```
```bash
db.movies.find()
```

4. ลองดู account บน admin database

```bash
use admin
```
```bash
db.getUsers()
```