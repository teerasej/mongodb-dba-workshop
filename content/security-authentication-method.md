# Authentication Method

## ผ่าน command line 

```bash
mongo admin -u <username> -p <password>
```

จาก log จะเห็นว่าเราถูก authenticate เข้ามาอยู่ในส่วนของ database `admin`

```bash
$ mongo admin -u pon -p pass
MongoDB shell version v4.0.2
connecting to: mongodb://127.0.0.1:27017/admin
MongoDB server version: 4.0.2
```

หรือจะ authenticate เพื่อเข้าใช้งาน database ที่ต้องการได้ผ่านคำสั่ง

```bash
mongo -u <pon> -p <password> --authenticationDatabase=admin
```

ซึ่งจะ authenticate เราเข้ามาใช้งานที่ database `test` โดยใช้ database `admin` เป็นตัว authenticate

จะเห็น log ประมาณนี้

```bash
Teerasej-MacBook-Pro:~ teerasejjiraphatchandej
$ mongo -u pon -p pass --authenticationDatabase=admin
MongoDB shell version v4.0.2
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 4.0.2
```

## จากภายใน mongo shell

```bash
shell> use admin
shell> db.auth('username','password')
```

## Note

ถ้ามีการสร้าง User ไว้ใน database นั้นๆ ตัว User ก็จะสามารถ authenticate เข้าใช้งาน database นั้นๆ ตามที่กำหนดได้