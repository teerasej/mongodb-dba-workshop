
# เชื่อมต่อ Mongo Shell กับ Cluster ตัวอย่างบน Atlas

เปิด Terminal หรือ Command Prompt

```bash
mongo "mongodb://cluster0-shard-00-00-jxeqq.mongodb.net:27017,cluster0-shard-00-01-jxeqq.mongodb.net:27017,cluster0-shard-00-02-jxeqq.mongodb.net:27017/test?replicaSet=Cluster0-shard-0" --authenticationDatabase admin --ssl --username m001-student --password m001-mongodb-basics
```

## รายละเอียด

- mongodb://cluster0-shard-00-00-jxeqq.mongodb.net:27017,cluster0-shard-00-01-jxeqq.mongodb.net:27017,cluster0-shard-00-02-jxeqq.mongodb.net:27017/
- `replicaSet`: Cluster0-shard-0
- `--authenticationDatabase`: admin
- `--ssl`
- `--username` : m001-student
- `--password` : m001-mongdb-basics

## คำสั่งพื้นฐาน

แสดงฐานข้อมูลทั้งหมด

```bash
show dbs
```

เลือกฐานข้อมูล

```bash
use <db>
```

แสดง collection ทั้งหมดในฐานข้อมูลที่ใช้งานอยู่

```bash
show collections
```

แสดง document ใน collection 

```bash
db.<collections>.find()
```

### แถม 

ลอง query ด้วย `.pretty()` ดู

```bash
db.<collections>.find().pretty()
```
