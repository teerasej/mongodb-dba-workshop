
# Authorization

> ต้องทำในส่วนของ [Authentication](authentication.md) ก่อนนะครับ
> 
## 1. เข้าใช้งานด้วย username และ password ของ  globalUserAdmin

1. เข้าใช้งาน mongo shell ด้วยการใช้ username และ password ที่เราสร้างไว้

```bash
mongosh -u globalUserAdmin -p  localhost:27017
```

2. สลับมาใช้งาน admin database

```bash
use admin
```
3. สร้าง User ที่สามารถดูข้อมูลบน sample_mflix database ได้อย่างเดียว

```bash
db.createUser(
  {
    user: "analystUser",
    pwd: passwordPrompt(),        
    roles: [
      { role: "read", db: "sample_mflix" },
    ]
  }
```

4. กรอกตั้งรหัสผ่านของ เมื่อมีการถาม 
5. เสร็จแล้วออกจาก mongo shell ด้วยการใช้คำสั่ง quit() หรือ ctrl + D

## 2. ทดสอบเข้าใช้งาน

1. เข้าใช้งาน mongo shell ด้วยการใช้ username และ password ที่เราสร้างไว้

```bash
mongosh "mongodb://analystUser@localhost:27017/sample_mflix?authSource=admin"
```

2. รันคำสั่งเพื่อแสดง collection ที่อยู่ใน sample_mflix database

```bash 
show collections
```

3. ทดสอบ query document ใน collection 

```bash
db.movies.findOne()
```
4. ออกจาก mongoshell session

```bash
quit()
```

## 3. ลบ Built-In Role ออกจาก database user

1. เข้าใช้งาน mongo shell ด้วย username และ password ของ globalUserAdmin

```bash
mongosh --username globalUserAdmin
```

2. สลับมาใช้งาน admin database

```bash
use admin
```

3. เช็คข้อมูลของ analystUser

```bash
db.getUser("analystUser")
```

4. ลบ read role ออกจาก sample_mflix โดยใช้คำสั่งด้านล่าง

```bash
db.revokeRolesFromUser(
    "analystUser",
    [
      { role: "read", db: "sample_mflix" }
    ]
)
```

5. เช็คข้อมูลของ analystUser อีกครั้ง

```bash
db.getUser("analystUser")
```

6. ออกจาก mongo shell

```bash
quit()
```