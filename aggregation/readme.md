
# Aggregation  

1. [เตรียมข้อมูล](import-data.md) 
2. [ใช้ Aggregation Builder ผ่าน MongoDB Compass](aggregation-builder.md)
3. [สร้าง View จาก Aggregation Pipeline](save-view.md)
4. [Export ไปใช้ใน code ต่างๆ](export-to-code.md)
5. [$lookup stage](lookup/readme.md)

## Workshop 

- [Workshop 1](workshop-aggregation-1.md)


## Note เกี่ยวกับ .explain('executionStats') ใน Aggregation

เนื่องจาก Mongo Compass รุ่น 1.20.5 ยังไม่ได้รองรับการทำ Explain plan ของ Aggregation เวลาต้องการวัดประสิทธิภาพ สามารถทำได้ผ่านคำสั่งของ Mongo shell เช่น

```bash
db.people.explain('executionStats').aggregate([])
```

** ใช้ได้ใน MongoDB 3.6 ขึ้นไป **

อ้างอิง - [StackOverflow](https://stackoverflow.com/questions/12702080/mongodb-explain-for-aggregation-framework)
