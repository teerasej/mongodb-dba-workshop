# Setting up a Replica Set

##1. สร้าง Config file สำหรับ 3 daemon

สร้างไฟล์ `node1.conf`

```bash
storage:
  dbPath: mongodb/db/node1
net:
  bindIp: 192.168.103.100,localhost
  port: 27001
security:
  authorization: enabled
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node1/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

### 1.1 สร้าง SSL key file 

key file จะถูกใช้เป็นกุญแจในการเชื่อมต่อ daemon เข้าในไปใน Replica Set เดียวกัน 
หาก daemon ไหน ไม่ได้กำหนดใช้ key file ชุดเดียวกัน จะไม่สามารถจัด set ได้

```bash
mkdir -p mongodb/pki/

chown vagrant:vagrant mongodb/pki/

openssl rand -base64 741 > mongodb/pki/keyfile

# ตั้งค่า permission ของไฟล์ SSL ให้รัดกุมกว่าปกติ ไม่งั้นจะรัน mongod ไม่ขึ้น
chmod 400 mongodb/pki/keyfile
```

### 1.2 สร้าง path สำหรับเก็บข้อมูล และรันใข้่งาน daemon

สร้าง db path สำหรับ node 1

```bash
mkdir -p mongodb/db/node1
```

รัน `mongod` ด้วยไฟล์ `node1.conf`

```bash
mongod -f node1.conf
```

### 1.3 สร้าง config file สำหรับ daemon 2 และ daemon 3 

Copy ไฟล์ `node1.conf` เป็น `node2.conf` และ `node3.conf`

```bash
cp node1.conf node2.conf
cp node2.conf node3.conf
```

แก้ไขไฟล์ `node2.conf` ในส่วน `dbpath`, `port`, `log path`

```bash
storage:
  dbPath: mongodb/db/node2
net:
  bindIp: 192.168.103.100,localhost
  port: 27002
security:
  authorization: enabled
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node2/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

แก้ไขไฟล์ `node3.conf` ในส่วน `dbpath`, `port`, `log path`

```bash
storage:
  dbPath: mongodb/db/node3
net:
  bindIp: 192.168.103.100,localhost
  port: 27003
security:
  authorization: enabled
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node3/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

สร้าง directory สำหรับ node2 และ node3

```bash
mkdir -p mongodb/db/node2
mkdir -p mongodb/db/node3
```

รัน mongod สำหรับ node2 และ node3

```bash
mongod -f node2.conf
mongod -f node3.conf
```

## 2. เริ่มสร้าง Replica Set

ต่อ shell เข้ากับ node1 (port 27001 ตามที่กำหนดไว้ใน config)

```bash
mongo --port 27001
```

ใช้คำสั่งเริ่ม replica set

```js
rs.initiate()
```

สร้าง user เพื่อใช้ในการเชื่อมต่อ Replica Set

```js
use admin
db.createUser({
  user: "nfadmin",
  pwd: "nfpass",
  roles: [
    {role: "root", db: "admin"}
  ]
})
```

ออกจาก shell  

```bash
exit
```

## 3. จัดชุด Replica Set 

ใช้ shell sign-in เข้า node1 ใน replica set "nf-example" (ตามที่ตั้งไว้ใน config file)

```
mongo --host "nf-example/192.168.103.100:27001" -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

รันคำสั่ง เช็คสถานะของ Replica Set

```js
rs.status()
```

เพิ่ม node 2 และ node 3 เข้า replica set

```bash
rs.add("192.168.103.100:27002")
rs.add("192.168.103.100:27003")
```

เช็ค Replica Set topology 

```bash
rs.isMaster()
```

สละตำแหน่ง primary node

```bash
rs.stepDown()
```

เช็ค Replica Set topology

```bash
rs.isMaster()
```

## 4. ทดสอบทำลาย node 1 ใน replica set

ให้เปิด terminal ขึ้นมาอีกอัน และใช้คำสั่งด้านล่าง เพื่อค้นหา และทำลาย daemon1

```bash
ps -ef | grep mongod
kill <pid>
```

สังเกตการเปลี่ยนแปลงของ Replica Set เช่น ถ้าตอนแรกเราใช้ Client อย่าง Mongo shell ต่อ daemon1 (port 27001) อาจจะไม่สามารถใช้งานได้อีกต่อไป 

ให้ออกจาก mongo shell และ login ใหม่เข้าไปใน daemon ที่เหลืออยู่ เช่น port 27002

```
mongo --host "nf-example/192.168.103.100:27002" -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```