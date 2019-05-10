# Setting up a shard cluster

## 1. สร้าง Replica Set สำหรับทำ Config Server

สร้างไฟล์ `csrs_1.conf`

```bash
sharding:
  clusterRole: configsvr
replication:
  replSetName: nf-csrs
security:
  keyFile: mongodb/pki/keyfile
net:
  bindIp: localhost,192.168.103.100
  port: 26001
systemLog:
  destination: file
  path: mongodb/db/csrs1.log
  logAppend: true
processManagement:
  fork: true
storage:
  dbPath: mongodb/db/csrs1
```

สร้างไฟล์​ `csrs_2.conf`

```bash
sharding:
  clusterRole: configsvr
replication:
  replSetName: nf-csrs
security:
  keyFile: mongodb/pki/keyfile
net:
  bindIp: localhost,192.168.103.100
  port: 26002
systemLog:
  destination: file
  path: mongodb/db/csrs2.log
  logAppend: true
processManagement:
  fork: true
storage:
  dbPath: mongodb/db/csrs2
```

สร้างไฟล์​  `csrs_3.conf`

```bash
sharding:
  clusterRole: configsvr
replication:
  replSetName: nf-csrs
security:
  keyFile: mongodb/pki/keyfile
net:
  bindIp: localhost,192.168.103.100
  port: 26003
systemLog:
  destination: file
  path: mongodb/db/csrs3.log
  logAppend: true
processManagement:
  fork: true
storage:
  dbPath: mongodb/db/csrs3
```

สร้าง directory สำหรับ Config server node ทั้ง 3 ตัว

```
mkdir -p mongodb/db/csrs1
mkdir -p mongodb/db/csrs2
mkdir -p mongodb/db/csrs3
```

เริ่ม server 3 ตัว

```bash
mongod -f csrs_1.conf
mongod -f csrs_2.conf
mongod -f csrs_3.conf
```

เชื่อมต่อ 1 ใน config server

```bash
mongo --port 26001
```

เริ่มต้น Replica Set ของ Config server

```bash
rs.initiate()
```

Creating super user on CSRS:

```bash
use admin
db.createUser({
  user: “nfadmin",
  pwd: “nfpass",
  roles: [
    {role: "root", db: "admin"}
  ]
})
```

Authenticate user

```bash
db.auth(“nfadmin", “nfpass")
```

เพิ่ม crsr 2 และ 3 เข้าไปใน Replica Set

```bash
rs.add("192.168.103.100:26002")
rs.add("192.168.103.100:26003")
```

## สร้าง MongoS Deamon

สร้างไฟล์ config Mongos (`mongos.conf`)

```bash
sharding:
  configDB: nf-csrs/192.168.103.100:26001,192.168.103.100:26002,192.168.103.100:26003
security:
  keyFile: mongodb/pki/keyfile
net:
  bindIp: localhost,192.168.103.100
  port: 26000
systemLog:
  destination: file
  path: mongodb/db/mongos.log
  logAppend: true
processManagement:
  fork: true
```

รัน mongoS

```bash
mongos -f mongos.conf
```

ต่อ shell เข้า mongos

```bash
mongo --port 26000 -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

ตรวจสอบสถานะการทำ Sharding

```bash
sh.status()
```

## 3. อัพเดตให้ Replica Set แรก มาอยู่ระบบ Shard

อัพเดต config ไฟล์ `node1.conf`

```bash
sharding:
  clusterRole: shardsvr
storage:
  dbPath: mongodb/db/node1
  wiredTiger:
    engineConfig:
      cacheSizeGB: .1
net:
  bindIp: 192.168.103.100,localhost
  port: 27001
security:
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node1/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-repl
```

อัพเดต config ไฟล์ `node2.conf`

```bash
sharding:
  clusterRole: shardsvr
storage:
  dbPath: mongodb/db/node2
  wiredTiger:
    engineConfig:
      cacheSizeGB: .1
net:
  bindIp: 192.168.103.100,localhost
  port: 27002
security:
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node2/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-repl
```

อัพเดต config ไฟล์ `node3.conf`

```bash
sharding:
  clusterRole: shardsvr
storage:
  dbPath: mongodb/db/node3
  wiredTiger:
    engineConfig:
      cacheSizeGB: .1
net:
  bindIp: 192.168.103.100,localhost
  port: 27003
security:
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node3/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-repl
```

เชื่อมต่อไปที่ node 2 (ใน workshop ก่อน node 2 นี้อาจจะถูกเลือกเป็น primary เราจะเลือก node นี้เพื่อแก้ไขก่อน):

```bash
mongo --port 27002 -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

ปิดการทำงานของ node

```bash
use admin
db.shutdownServer()
```

รัน node ด้วย configuration ใหม่

```bash
mongod -f node2.conf
```

สั่งให้สละ primary

```bash
rs.stepDown()
```

**ทำแบบเดียวกับ node 3 และ node 1 ที่เหลือ**

เชื่อมต่อกลับเข้า mongoS 

```bash
mongo --port 26000 -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

เพิ่ม Shard เข้า mongoS

```bash
sh.addShard(“nf-repl/192.168.103.100:27002")
```
