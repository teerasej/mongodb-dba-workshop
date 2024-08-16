# Enable Auditing Log

## 1. เปิดไฟล์ mongod.conf

1. เปิดไฟล์ mongod.conf

### Windows 

เปิดไฟล์ `C:\Program Files\MongoDB\Server\7.0\bin\mongod.cfg` ด้วย Editor ที่ถนัด

### MacOS 

ในที่นี้ถ้าเราใช้ homebrew ในการติดตั้ง log จะอยู่แตกต่างกัน[ตามระบบ mac ที่ใช้](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) 

Intel chip: 
```
/usr/local/etc/mongod.conf
```
Apple chip (M)
```
/opt/homebrew/etc/mongod.conf
```

2. เพิ่มส่วนนี้เข้าไปในไฟล์ configuration

```bash
auditLog:
  destination: file
  format: JSON
  path: <path-to-log-file>/auditLog.json
```


## 2. ทำการ restart mongod

ทำการปิดและเปิดการทำงานของ MongoDB ใหม่


## 3. เช็คไฟล์ log ที่เราสร้างไว้