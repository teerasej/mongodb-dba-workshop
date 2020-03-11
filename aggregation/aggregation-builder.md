
# ใช้ Aggregation Builder ผ่าน MongoDB Compass

> ควรทำการ [import ข้อมูลเข้า Cluster แล้ว](import-data.md)

1. เชื่อมต่อ Mongo Compass เข้า Cluster `localhost:27017`
2. เลือก collection `example.air_airlines`
3. เลือก Tab **Aggregations**

<img width="830" alt="agg-builder-select-stage" src="https://user-images.githubusercontent.com/85179/76435011-0cb5eb00-63e9-11ea-9edb-5f6aeaa2abf7.png">

4. เลือก Pipeline stage `$match` และกำหนดค่าดังนี้ (ดู [$match](https://docs.mongodb.com/manual/reference/operator/aggregation/match/) เพิ่มเติม)

```
{
  country: "Mexico",
}
```

เป็นการกำหนดค่าเพื่อเลือก document มีข้อมูลตรงกับที่ต้องการ

5. กดปุ่ม **Add Stage** ด้านล่าง
6. เลือก Pipeline stage `$project` และกำหนดค่าดังนี้ (ดู [$project](https://docs.mongodb.com/manual/reference/operator/aggregation/project/) เพิ่มเติม)

```
{
  airline: 1,
  name: 1,
  country: 1
}
```

เป็นการเลือก field ทีต้องการใน document เพื่อนำไปใช้งาน

ทดสอบดูผลลัพธ์


