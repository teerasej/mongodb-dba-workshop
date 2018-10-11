# Setting up a Replica Set

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

สร้าง SSL key file 

```bash
sudo mkdir -p mongodb/pki/

sudo chown vagrant:vagrant mongodb/pki/

openssl rand -base64 741 > mongodb/pki/keyfile

chmod 400 mongodb/pki/keyfile
```

สร้าง db path สำหรับ node 1

```bash
mkdir -p mongodb/db/node1
```

รัน `mongod` ด้วยไฟล์ `node1.conf`

```bash
mongod -f node1.conf
```

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
mkdir -p mongodb/db/{node2, node3}
```

รัน mongod สำหรับ node2 และ node3

```bash
mongod -f node2.conf
mongod -f node3.conf
```

ต่อ shell เข้ากับ node1

```bash
mongo --port 27001
```

ใช้คำสั่งเริ่ม replica set

```js
rs.initiate()
```

สร้าง user

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

ออกจาก shell และเชื่อมต่อ replica set ทั้งหมด

```bash
exit

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
