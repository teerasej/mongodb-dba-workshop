# The Localhost Exception

ทดลองรันคำสั่ง

```bash
mongod --auth
```

เป็นการบังคับให้ client ทุกตัวที่เชื่อมต่อเข้า daemon นี้ ต้องมีการผ่านการ Authenticate ทุกครั้ง

จากนั้นใช้ mongo shell ต่อเข้า mongod 
จะพบว่าเราไม่สามารถรันคำสั่งใดๆ ในการแก้ไขข้อมูลได้

- หลังจากติดตั้ง MongoDB ในฐานข้อมูลจะไม่มี user ใดๆ อยู่เลย
- แล้วถ้าเรารัน mongod แบบ --auth เราจะสามารถสร้าง user ได้ยังไง?
- MongoDB จึงมีกฎยกเว้นอยู่ เรียกว่า Localhost Exception 
- ซึ่งจะอนุญาตให้ client ที่ login เข้า mongod บนเครื่องเดียวกัน (localhost) มีสิทธิ์สร้าง User แรกใน Cluster นั้น

```bash
use admin
db.createUser({ user: "pon", pwd: "pass", roles: [{role: "userAdminAnyDatabase", db: "admin"}]})
```

สังเกตว่า เรายังไม่สามารถแก้ไขข้อมูลได้เหมือนเดิม
ต้องรันคำสั่ง authenticate user ก่อน

```bash
db.auth('pon','pass')
```

และสามารถดู User ได้

```bash
db.system.users.find()
```
