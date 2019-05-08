# MongoD Configuration File

- [Command line options](https://docs.mongodb.com/manual/reference/program/mongod/#options)
- [Config file options](https://docs.mongodb.com/manual/reference/configuration-options)

## คำสั่งโหลด configuration file

```bash
mongod --config "/etc/mongod.conf"

mongod -f "/etc/mongod.conf"
```

## ตัวอย่าง YAML 

```bash
storage:
  dbPath: "/data/db"
systemLog:
  path: "/data/log.mongod.log"
  destination: "file"
replication:
  replSetName: NF100
net:
  bindIp : "127.0.0.1, 192.168.0.10"
ssl:
  mode: "requireSSL"
  PEMKeyFile: "/etc/ssl/ssl.pem"
  CAFile: "/etc/ssl/SSLCA.pem"
security:
  keyFile: "/data/keyfile"
processManagement:
  fork : true
```


## Workshop สร้าง config file

1. รัน `vagrant ssh`
2. ดูข้อมูลใน `/etc` ด้วยคำสั่งด้านล่าง จะเห็นว่ามีไฟล์ `mongod.conf` อยู่

```bash
ls /etc
```

3. ใช้ vim เปิดดู

```bash
vim /etc/mongod.conf
```

4. กด `i` เพื่อเข้าสู่ insert mode
5. กดปุ่ม `esc` และกด `:q!` เพื่อออกโดยไม่แก้ไขอะไร
6. ใช้คำสั่ง `vim` เพื่อสร้างไฟล์ใหม่

```bash
vim
```

7. เพิ่ม comment `# hello`
8. กดปุ่ม `esc` และกด `:w mongo.conf` เพื่อบันทึกไฟล์ ชื่อ `mongo.conf`
	- หรือกดปุ่ม `esc` และกด `:x` เพื่อบันทึกไฟล์ และปิด vim
	- หรือกดปุ่ม `esc` และกด `:w newname` (หรือ `:x newname` เพื่อบันทึกไฟล์แบบ Save As)
	- หรือกดปุ่ม `esc` และกด `:q!` เพื่อออกโดยไม่แก้ไขอะไร
9. ใช้คำสั่ง `ls` เพื่อดูว่ามีไฟล์ชื่อ `mongo.conf`
10. ใช้คำสั่ง `vim mongo.conf` เพื่อเปิดไฟล์มาแก้ไขอีกครั้ง
11. กด `i` เพื่อเข้าโหมดแก้ไข
12. สร้าง config file

```bash
storage:
  dbPath: "/data/db"
systemLog:
  path: "/data/mongo.log"
  destination: "file"
replication:
  replSetName: NF100
processManagement:
  fork : true
```

13. กดปุ่ม `esc` และกด `:x` เพื่อบันทึกไฟล์ และปิด vim
14. ทดสอบรัน mongo โดยใช้ config ใหม่

```bash
mongod -f "mongo.conf"
```

## คำสั่งค้นหา pid ของ process mongod ในกรณีที่ต้องการเคลียร์ทิ้ง

ค้นหา pid ของ MongoD

```bash
ps -ef | grep mongod
```

เมื่อทราบ pid แล้วใช้คำสั่ง

```bash
kill <pid>
```