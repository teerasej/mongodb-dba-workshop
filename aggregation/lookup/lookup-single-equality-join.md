
# Single JOIN

- เราสามารถใช้ document ใน `orders` collection เป็นตัวตั้ง 
- และนำ document จาก `inventory` collection มารวมในผลลัพธ์ 
- โดยใช้ `$lookup` stage กำหนด `localField` เป็น `item` field ของ orders collection
- และกำหนด `foreignField` เป็น `sku` ของ inventory collection 
- `$lookup` stage จะเทียบค่าที่กำหนด และรวม document จาก `inventory` collection เข้าไปใน `orders` document ในผลลัพธ์


1. ใช้ Mongo shell ต่อเข้า Local Cluster ([วิธีการรัน Mongo Daemon](../mongod-command.md), [วิธีการเชื่อมต่อ Cluster ด้วย Mongo shell](../connect-mongodb-with-shell.md))
2. สร้าง Database `store`

```bash
use store
```

3. เพิ่มข้อมูลลง Collection `orders`

```js
db.orders.insert([
   { "_id" : 1, "item" : "almonds", "price" : 12, "quantity" : 2 },
   { "_id" : 2, "item" : "pecans", "price" : 20, "quantity" : 1 },
   { "_id" : 3  }
])
```

4. เพิ่มข้อมูลสินค้าลง collection `inventory`

```js
db.inventory.insert([
   { "_id" : 1, "sku" : "almonds", description: "product 1", "instock" : 120 },
   { "_id" : 2, "sku" : "bread", description: "product 2", "instock" : 80 },
   { "_id" : 3, "sku" : "cashews", description: "product 3", "instock" : 60 },
   { "_id" : 4, "sku" : "pecans", description: "product 4", "instock" : 70 },
   { "_id" : 5, "sku": null, description: "Incomplete" },
   { "_id" : 6 }
])
```

5. เปิด Mongo Compass และเชื่อมต่อมาที่ Local Cluster
6. เลือก database `store` และ collection `orders` (เรียกอีกแบบว่า namespace `store.orders`)

7. เปิดส่วน Aggregation และเลือก `$lookup` stage

```js
{
    from: "inventory",
    localField: "item",
    foreignField: "sku",
    as: "inventory_docs"
}
```

8. เทียบและสังเกตผลลัพธ์

```json
{
   "_id" : 1,
   "item" : "almonds",
   "price" : 12,
   "quantity" : 2,
   "inventory_docs" : [
      { "_id" : 1, "sku" : "almonds", "description" : "product 1", "instock" : 120 }
   ]
}
{
   "_id" : 2,
   "item" : "pecans",
   "price" : 20,
   "quantity" : 1,
   "inventory_docs" : [
      { "_id" : 4, "sku" : "pecans", "description" : "product 4", "instock" : 70 }
   ]
}
{
   "_id" : 3,
   "inventory_docs" : [
      { "_id" : 5, "sku" : null, "description" : "Incomplete" },
      { "_id" : 6 }
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