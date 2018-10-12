# Workshop Internal Authentication

สร้าง key file

```bash
openssl rand -base64 755 > keyfile
chmod 400 keyfile
```

สร้าง directory เก็บไฟล์ฐานข้อมูลของ daemon 3 ตัว

```bash
mkdir -p rs1/db rs2/db rs3/db
```

รัน daemon แรก 

```bash
mongod --replSet nfRplSet --dbpath rs1/db --logpath rs1/db/mongod.log --port 27017 --fork --keyFile keyfile
```

Daemon 2

```bash
mongod --replSet nfRplSet --dbpath rs2/db --logpath rs2/db/mongod.log --port 27018 --fork --keyFile keyfile
```

Daemon 3

```bash
mongod --replSet nfRplSet --dbpath rs3/db --logpath rs3/db/mongod.log --port 27019 --fork --keyFile keyfile
```

เสร็จแล้วใช้คำสั่ง mongo ต่อเข้า deamon 1 (port 27017)

```bash
mongo
```

 จะเจอ error เพราะการใช้ keyfile เป็นการ force ให้ daemon ใช้ authentication 

```bash
rs.initiate()
```

ให้ใช้คำสั่งเข้าไปสร้าง user ใน daemon

```bash
use admin
db.createUser({ user: 'pon', pwd: 'pass', roles: ['root']})
db.auth('pon','pass')
```

ออกมาจาก shell และใช้คำสั่งเริ่ม Replica Set

```
exit

mongo --host "nfRplSet/127.0.0.1:27017" -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

```
mongo
```

และลองสัั่งดู `rs.status()`

และสั่งเพิ่ม daemon เข้าไปใน Replica Set

```
rs.add("127.0.0.1:27018")
rs.add("127.0.0.1:27019")
```

## เคลียร์

```bash
rm -rf rs1 rs2 rs3 keyfile
```
