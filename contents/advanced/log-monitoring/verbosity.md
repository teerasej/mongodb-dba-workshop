
# Verbosity of Component 

## 0. Setup environment 

ให้แน่ใจว่าได้

1. ทำตามขั้นตอนใน [mongodump](../tools/mongodump.md) เรียบร้อยแล้ว
2. ทำตามขั้นตอนใน [mongorestore](../tools/mongorestore.md) เรียบร้อยแล้ว

## 1. เปิดไฟล์ mongod.conf

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

## 2. ตั้งค่า Verbosity ของ Component ใน mongod.conf

ทำการเพิ่มค่าด้านล่างลงไปในไฟล์ และบันทึกไฟล์

```conf
systemLog:
  destination: file
  logAppend: true
  path:  ...
  verbosity: 0
  component:
    index:
      verbosity: 1
```

## 3. restart MongoDB server

1. ทำการหยุดการทำงานของ MongoDB server และเริ่มการทำงานใหม่ เพื่อให้การเปลี่ยนแปลงการตั้งค่าที่เราทำไปมีผล
   
## 4. เช็ค log ที่เราตั้งค่าไว้ว่ามีการเปลี่ยนแปลงหรือไม่  

### Windows 

1. โดยปกติ Log จะอยู่ที่ `C:\Program Files\MongoDB\Server\<version>\log\mongod.log` 
2. เปิดโดยใช้เครื่องมือที่ถนัด และหา keyword `"s":"D1", "c":"INDEX"` ใน log file โดย scroll มาช่วงล่างๆ ที่เป็น log ล่าสุด ซึ่ง D1 คือ debug level 1 ได้มาจากค่า verbosity ที่เราตั้งไว้

### MacOS

1. ในที่นี้ถ้าเราใช้ homebrew ในการติดตั้ง log จะอยู่แตกต่างกัน[ตามระบบ mac ที่ใช้](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) 

 Intel chip: 
```
/usr/local/var/log/mongodb
```
 Apple chip (M)
```
/opt/homebrew/var/log/mongodb
```

1. เปิดโดยใช้เครื่องมือที่ถนัด และหา keyword `"s":"D1", "c":"INDEX"` ใน log file โดย scroll มาช่วงล่างๆ ที่เป็น log ล่าสุด ซึ่ง D1 คือ debug level 1 ได้มาจากค่า verbosity ที่เราตั้งไว้