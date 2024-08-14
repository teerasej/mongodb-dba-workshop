# Wildcard Index

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. เพิ่มข้อมูลใหม่ผ่าน MongoCompass

1. จากหน้าจอหลักของ Compass ให้เลือก database **sample_mflix** 
2. กดเปิด mongosh จากขอบด้านล่างสุดของหน้าจอ
3. ใช้คำสั่ง insert ข้อมูลใหม่เข้าไปใน collection **products** ดังนี้

```js
db.products.insertMany([
  {
    _id: new ObjectId("64a36318574fd20cd8fb9798"),
    sku: 111,
    product_name: "Stero Speakers",
    price: 100,
    stock: 5,
    product_attributes: { color: "black", size: "5x5x5", weight: "5lbs" },
  },
  {
    _id: new ObjectId("64a36318574fd20cd8fb9799"),
    sku: 121,
    product_name: "Bread",
    price: 2,
    stock: 50,
    product_attributes: {
      type: "white",
      calories: 100,
      weight: "24g",
      crust: "soft",
    },
  },
  {
    _id: new ObjectId("64a36318574fd20cd8fb979a"),
    sku: 131,
    product_name: "Milk",
    price: 3,
    stock: 20,
    product_attributes: {
      type: "2%",
      calories: 120,
      weight: "1L",
      brand: "Dairy Farmers",
    },
  },
]);
```

### 2. ทดสอบการสร้าง Wildcard Index

1. จาก database **sample_mflix** ให้เลือก **products** collection มาใช้ทดสอบ
2. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
3. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **product_attributes.$**** และกดสร้าง
4. กลับมาที่ tab **documents** ให้ทำการเลือก Query 
5. ในช่อง Query ให้ใส่รายละเอียดคำสั่งดังนี้ และกดปุ่ม **Find**

```js
{
  "product_attributes.crust": false,
}
```

6. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (มีการใช้ wildcard index)
   2. Document examined
   3. Document returned
   4. Execution Time