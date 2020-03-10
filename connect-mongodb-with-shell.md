# รัน MongoDB ด้วย Shell

## สำหรับ MacOS

1. เปิดโปรแกรม **Terminal** 
2. รันคำสั่งด้านล่าง เพื่อสร้าง โฟลเดอร์สำหรับเก็บฐานข้อมูล (ในที่นี่อ้างอิงจาก default location ของระบบ) ใช้ sudo ถ้าจำเป็น

```bash
mkdir -p ~/data/db

// ถ้าติด Permission denied ให้ลองใช้ sudo 
sudo mkdir -p ~/data/db
```

3. รันคำสั่งด้านล่าง และกรอกรหัสผ่านของคุณ

```
sudo chown -R `id -un` /mongo/db
```

4. รันคำสั่ง `mongod --dbpath ~/data/db` เพื่อรันตัว Database server 

## สำหรับ Windows

1. สร้างโฟลเดอร์เปล่าขึ้นมาที่ `C:\data\db`
2. เปิด Command Prompt 
3. รันคำสั่ง

```
mongod --dbpath "C:\data\db"
```
** ขั้นตอนนี้ต้อง set path ในส่วนของ System Environment ให้เรียบร้อย [ดูวิธีการได้ที่](https://nextflow.in.th/2018/prepare-mongodb-for-database-administrator-dba/)

** ถ้าไม่ได้ตั้งค่า path จะรันคำสั่งด้านบนไม่ได้ ให้ไปรันจากโฟลเดอร์ที่ติดตั้ง MongoDB เช่น 

```
C:\Program Files\MongoDB\Server\4.0\bin
```

### Daemon เริ่มทำงาน

จะเห็น log แสดงประมาณด้านล่าง

```bash
2018-10-08T13:59:12.686+0700 I CONTROL  [initandlisten] MongoDB starting : pid=2029 port=27017 dbpath=/data/db 64-bit host=Teerasej-MacBook-Pro.local
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] db version v3.4.4
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] git version: 888390515874a9debd1b6c5d36559ca86b44babd
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] OpenSSL version: OpenSSL 1.0.2p  14 Aug 2018
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] allocator: system
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] modules: none
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] build environment:
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten]     distarch: x86_64
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten]     target_arch: x86_64
2018-10-08T13:59:12.687+0700 I CONTROL  [initandlisten] options: {}
2018-10-08T13:59:12.687+0700 I -        [initandlisten] Detected data files in /data/db created by the 'wiredTiger' storage engine, so setting the active storage engine to 'wiredTiger'.
2018-10-08T13:59:12.687+0700 I STORAGE  [initandlisten] wiredtiger_open config: create,cache_size=7680M,session_max=20000,eviction=(threads_min=4,threads_max=4),config_base=false,statistics=(fast),log=(enabled=true,archive=true,path=journal,compressor=snappy),file_manager=(close_idle_time=100000),checkpoint=(wait=60,log_size=2GB),statistics_log=(wait=0),
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] ** WARNING: soft rlimits too low. Number of files is 256, should be at least 1000
2018-10-08T13:59:13.100+0700 I FTDC     [initandlisten] Initializing full-time diagnostic data capture with directory '/data/db/diagnostic.data'
2018-10-08T13:59:13.100+0700 I NETWORK  [thread1] waiting for connections on port 27017
```

ให้สังเกต log ช่วงสุดท้าย `waiting for connections on port 27017` แสดงถึง Server ที่รอรับการเชื่อมต่อ

จากนั้นให้เปิด Terminal หรือ Command Prompt อีกหน้าต่างหนึ่ง และรันคำสั่ง `mongo` เพื่อเปิดใช้งาน Mongo Shell ถ้าถูกต้องจะเห็น log ประมาณด้านล่าง

```bash
Teerasej-MacBook-Pro:~ teerasejjiraphatchandej$ mongo
MongoDB shell version v3.4.4
connecting to: mongodb://127.0.0.1:27017
MongoDB server version: 3.4.4
Server has startup warnings: 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] ** WARNING: Access control is not enabled for the database.
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] **          Read and write access to data and configuration is unrestricted.
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] 
2018-10-08T13:59:13.097+0700 I CONTROL  [initandlisten] ** WARNING: soft rlimits too low. Number of files is 256, should be at least 1000
> 
```

ลองกลับมาดูที่หน้าต่างเดิม ที่เราสั่งรัน mongod ไว้ จะเห็น log แสดงการเชื่อมต่อเข้ามาจาก mongo shell 

```bash
2018-10-08T14:01:37.053+0700 I NETWORK  [thread1] connection accepted from 127.0.0.1:52690 #1 (1 connection now open)
2018-10-08T14:01:37.055+0700 I NETWORK  [conn1] received client metadata from 127.0.0.1:52690 conn1: { application: { name: "MongoDB Shell" }, driver: { name: "MongoDB Internal Client", version: "3.4.4" }, os: { type: "Darwin", name: "Mac OS X", architecture: "x86_64", version: "18.0.0" } }
```
