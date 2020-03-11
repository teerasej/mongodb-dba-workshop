

# Workshop 1 

> ควรทำการ [import ข้อมูลเข้า Cluster แล้ว](import-data.md)

1. เชื่อมต่อ Mongo Compass เข้า Cluster `localhost:27017`
2. เลือก collection `example.air_airlines`
3. เลือก Tab **Aggregations**

<img width="830" alt="agg-builder-select-stage" src="https://user-images.githubusercontent.com/85179/76435011-0cb5eb00-63e9-11ea-9edb-5f6aeaa2abf7.png">

4. เลือก Pipeline stage `$group` และกำหนดค่าดังนี้ (ดู [$group](https://docs.mongodb.com/manual/reference/operator/aggregation/group/) เพิ่มเติม)

```
{
  _id: {
      active: '$active',
      country: '$country'
  },
  flightCount: { $sum: 1 }
}
```

เป็นการจัด group ตาม field ชื่อ `active` และ `country` 

และกำหนด field ชื่อ `flightCount` โดยนับจำนวน document ตามการจัดกลุ่มดังกล่าว

5. กดปุ่ม **Add Stage** ด้านล่าง
6. เลือก Pipeline stage `$match` และกำหนดค่าดังนี้ (ดู [$match](https://docs.mongodb.com/manual/reference/operator/aggregation/match/) เพิ่มเติม)

```
{
  flightCount: { $gte: 5 }
}
```

เป็นการเลือก document ที่มี flightCount จาก stage ก่อนหน้า ที่มีจำนวนมากกว่า 5

ทดสอบดูผลลัพธ์


