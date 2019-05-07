# MongoD

- daemon คือ process ของ Mongo ที่รันเป็น background
- รัน daemon ได้ด้วยคำสั่ง `mongod`
- port เริ่มต้นคือ 27017
- path เริ่มต้นคือ `/data/db`
- `--port` กำหนด port
- `--dbpath` กำหนด directory เก็บ database file
- `--logpath` กำหนดที่อยู่เก็บ log ไฟล์
- `--fork` รัน mongod เป็น background process
	 
## คำสั่งปิด mongo daemon จาก shell อีกอันหนึ่ง

```bash
mongo admin --eval 'db.shutdownServer()'
```

## คำสั่งสร้าง directory ใหม่ 
```bash
// สร้าง directory
mkdir first_mongo

// ทดสอบรัน daemon ด้วย **port** และ **dbpath** ใหม่ 
mongod --port 30000 --dbpath first_mongod --fork
```

## คำสั่งรันแบบ เก็บ log ไฟล์

```bash
mongod --port 30000 --dbpath first_mongod --logpath first_mongod/mongod.log --fork
```

## คำสั่งเชื่อมต่อ mongo shell เข้า port 30000

```bash
mongo --port 30000
```

## คำสั่งปิด server จาก shell

```bash
mongo admin --port 30000 --eval 'db.shutdownServer()'
```
