
# การเข้าใช้งาน Log ของ MongoDB บนเครื่องเซิฟเวอรของเราเอง

## ที่อยู่ของไฟล์ log (Windows)

```
C:\Program Files\MongoDB\Server\<version>\log
```

## การใช้งาน mongo shell 

> [ดูวิธีการรัน MongoDB instance บน Windows & MacOS ได้จากที่นี่](https://github.com/teerasej/mongodb-dba-workshop/blob/master/contents/connect-mongodb-with-shell.md) 

1. เปิด Command Prompt และเข้าไปที่โฟลเดอร์ที่ติดตั้ง MongoDB เช่น ใช้คำสั่ง 

```
cd C:\Program Files\MongoDB\Server\7.0\bin
```

2. พิมพ์คำสั่งดังนี้ เพื่อเริ่มการทำงานของ MongoDB server

```
mongod 
```


3. เปิด command prompt อีกหน้าต่าง เพื่อใช้คำสั่ง mongosh ในการเชื่อมต่อเข้า mongodb server ที่ทำงานอยู่บน local server

```
cd C:\Program Files\MongoDB\Server\7.0\bin
```

```
mongosh
```

4. ใช้คำสั่งด้านล่างเพื่อแสดงรายการของ log ทั้งหมด

```
show logs
```

5. ใช้คำสั่งด้านล่างเพื่อแสดง log ประเภท startupWarnings

```
show log startupWarnings
```

จะทำให้เห็นว่ามี log ที่เกิดขึ้นในระหว่างการเริ่มต้น MongoDB server

```bash
[
  '{"t":{"$date":"2024-08-15T01:19:47.577+00:00"},"s":"W",  "c":"CONTROL",  "id":22120,   "ctx":"initandlisten","msg":"Access control is not enabled for the database. Read and write access to data and configuration is unrestricted","tags":["startupWarnings"]}\n'
]
```
