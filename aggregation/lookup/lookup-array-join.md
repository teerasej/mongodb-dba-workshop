
# Array JOIN

ใน Mongo 3.4+ เราสามารถใช้ `localField` เป็น Array เพื่อเทียบตรงกับค่าพื้นฐานกับ `foreignField` ได้

1. ใช้ Mongo shell ต่อเข้า Local Cluster ([วิธีการรัน Mongo Daemon](../mongod-command.md), [วิธีการเชื่อมต่อ Cluster ด้วย Mongo shell](../connect-mongodb-with-shell.md))
2. สร้าง Database `store`

```bash
use school
```

3. เพิ่มข้อมูลลง Collection `classes`

```js
db.classes.insert( [
   { _id: 1, title: "Reading is ...", enrollmentlist: [ "giraffe2", "pandabear", "artie" ], days: ["M", "W", "F"] },
   { _id: 2, title: "But Writing ...", enrollmentlist: [ "giraffe1", "artie" ], days: ["T", "F"] }
])
```

4. เพิ่มข้อมูลสินค้าลง collection `members`

```js
db.members.insert( [
   { _id: 1, name: "artie", joined: new Date("2016-05-01"), status: "A" },
   { _id: 2, name: "giraffe", joined: new Date("2017-05-01"), status: "D" },
   { _id: 3, name: "giraffe1", joined: new Date("2017-10-01"), status: "A" },
   { _id: 4, name: "panda", joined: new Date("2018-10-11"), status: "A" },
   { _id: 5, name: "pandabear", joined: new Date("2018-12-01"), status: "A" },
   { _id: 6, name: "giraffe2", joined: new Date("2018-12-01"), status: "D" }
])
```

5. เปิด Mongo Compass และเชื่อมต่อมาที่ Local Cluster
6. เลือก database `school` และ collection `classes` (เรียกอีกแบบว่า namespace `school.classes`)

7. เปิดส่วน Aggregation และเลือก `$lookup` stage

```js
{
   from: "members",
   localField: "enrollmentlist",
   foreignField: "name",
   as: "enrollee_info"
}
```

8. เทียบและสังเกตผลลัพธ์

```json
{
   "_id" : 1,
   "title" : "Reading is ...",
   "enrollmentlist" : [ "giraffe2", "pandabear", "artie" ],
   "days" : [ "M", "W", "F" ],
   "enrollee_info" : [
      { "_id" : 1, "name" : "artie", "joined" : ISODate("2016-05-01T00:00:00Z"), "status" : "A" },
      { "_id" : 5, "name" : "pandabear", "joined" : ISODate("2018-12-01T00:00:00Z"), "status" : "A" },
      { "_id" : 6, "name" : "giraffe2", "joined" : ISODate("2018-12-01T00:00:00Z"), "status" : "D" }
   ]
}
{
   "_id" : 2,
   "title" : "But Writing ...",
   "enrollmentlist" : [ "giraffe1", "artie" ],
   "days" : [ "T", "F" ],
   "enrollee_info" : [
      { "_id" : 1, "name" : "artie", "joined" : ISODate("2016-05-01T00:00:00Z"), "status" : "A" },
      { "_id" : 3, "name" : "giraffe1", "joined" : ISODate("2017-10-01T00:00:00Z"), "status" : "A" }
   ]
}
```

## เทียบกับ SQL 

วิธีการนี้ เทียบกับ SQL statement ด้านล่าง

```sql
SELECT *, inventory_docs
FROM orders
WHERE inventory_docs IN (SELECT *
FROM inventory
WHERE sku= orders.item);
```