# Reconfiguring a Running Replica Set

## 1. สร้าง Node 4 และ Arbiter Node เพิ่มเข้าไปใน Replica Set เพื่อสังเกตผล

สร้างไฟล์ config สำหรับ `node4.conf`

```bash
storage:
  dbPath: mongodb/db/node4
net:
  bindIp: 192.168.103.100,localhost
  port: 27004
security:
  authorization: enabled
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/node4/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

สร้างไฟล์ สำหรับ `arbiter.conf`

```bash
storage:
  dbPath: mongodb/db/arbiter
net:
  bindIp: 192.168.103.100,localhost
  port: 28000
security:
  authorization: enabled
  keyFile: mongodb/pki/keyfile
systemLog:
  destination: file
  path: mongodb/db/arbiter/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

สร้าง directory สำหรับ node4 และ arbiter

```bash
mkdir -p mongodb/db/node4
mkdir -p mongodb/db/arbiter
```

รัน `mongod` สำหรับ `node 4` และ `arbiter`

```bash
mongod -f node4.conf
mongod -f arbiter.conf
```

ใช้ mongo shell 

```
mongo --host "nf-example/192.168.103.100:27001" -u "nfadmin" -p "nfpass" --authenticationDatabase "admin"
```

จาก shell ให้เพิ่ม node 4 และ arbiter node เข้า replica set

```bash
rs.add("192.168.103.100:27004")
rs.addArb("192.168.103.100:28000")
```

เช็คสถานะของ Replica Set สังเกตค่าที่เปลี่ยนแปลงไปใน Set

```bash
rs.isMaster()
rs.status()
```

## 2. ลดสมาชิกของ Replica Set

ลบ Arbiter node ออกจาก Replica Set

```bash
rs.remove("192.168.103.100:28000")
```

เช็คสถานะของ Replica Set สังเกตค่าที่เปลี่ยนแปลงไปใน Set

```bash
rs.isMaster()
rs.status()
```

## 3. ทดลองปรับแต่งการทำงานของ Node ที่อยู่ใน Replica Set

ดึงค่า configuration ของ Replica Set มาเก็บไว้ในตัวแปรของ Shell

```bash
cfg = rs.conf()
```

แก้ไขค่า config ของ Node ใหม่ 

ตาม Workshop คือ node 4 (Replica Set นับ Nodeตัวแรกเป็น cfg.members[0]) แต่จะสามารถทดลองกับ Node 1,2,3 ก็ได้

```bash
cfg.members[3].votes = 0
cfg.members[3].hidden = true
cfg.members[3].priority = 0
```

สั่งให้ Replica Set โหลด config ตัวใหม่ไปใช้งาน

```bash
rs.reconfig(cfg)
```

เช็คสถานะของ Replica Set สังเกตค่าที่เปลี่ยนแปลงไปใน Set

```bash
rs.isMaster()
rs.status()
```

**การแก้ไข topology ของ Replica Set จะทำให้เกิดการ election ขึ้นใหม่**