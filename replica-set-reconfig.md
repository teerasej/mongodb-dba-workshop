# Reconfiguring a Running Replica Set

สร้างไฟล์ config สำหรับ `node4.conf`

```bash
storage:
  dbPath: mongodb/db/node4
net:
  bindIp: 192.168.103.100,localhost
  port: 27004
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
systemLog:
  destination: file
  path: mongodb/db/arbiter/mongod.log
  logAppend: true
processManagement:
  fork: true
replication:
  replSetName: nf-example
```

รัน `mongod` สำหรับ `node 4` และ `arbiter`

```bash
mongod -f node4.conf
mongod -f arbiter.conf
```

จาก shell ให้เพิ่ม node 4 และ arbiter เข้า replica set

```bash
rs.add("192.168.103.100:27004")
rs.addArb("192.168.103.100:28000")
```

เช็คสถานะของ Replica Set

```bash
rs.isMaster()
```

ลบ arbiter ออกจาก Replica Set

```bash
rs.remove("192.168.103.100:28000")
```

ดึงค่า configuration ของ Replica Set มาเก็บไว้ในตัวแปรของ Shell

```bash
cfg = rs.conf()
```

แก้ไขค่า config ใหม่ (node 4)

```bash
cfg.members[3].votes = 0
cfg.members[3].hidden = true
cfg.members[3].priority = 0
```

สั่งให้ Replica Set โหลด config ตัวใหม่ไปใช้งาน

```bash
rs.reconfig(cfg)
```

**การแก้ไข topology ของ Replica Set จะทำให้เกิดการ election ขึ้นใหม่**