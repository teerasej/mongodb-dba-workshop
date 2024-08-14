# Sparse Index

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. เพิ่มข้อมูลใหม่ผ่าน MongoCompass

1. จากหน้าจอหลักของ Compass ให้เลือก database **sample_mflix** 
2. กดเปิด mongosh จากขอบด้านล่างสุดของหน้าจอ
3. ใช้คำสั่ง insert ข้อมูลใหม่เข้าไปใน collection **sparseExample** ดังนี้

```js
db.sparseExample.insertMany([
  {
    _id: new ObjectId("64920144bf3922c17f7181ca"),
    username: "coolUser",
    avatar_url: "https://api.multiavatar.com/coolUser.svg",
  },
  {
    _id: new ObjectId("64920144bf3922c17f7181cb"),
    username: "testUser",
    avatar_url: "https://api.multiavatar.com/testUser.svg",
  },
  {
    _id: new ObjectId("64920144bf3922c17f7181cc"),
    username: "anotherUser",
    avatar_url: "https://api.multiavatar.com/anotherUser.svg",
  },
  { _id: new ObjectId("64920173bf3922c17f7181cd"), username: "test" },
]);
```

### 2. ทดสอบการสร้าง Sparse Index

1. จาก database **sample_mflix** ให้เลือก **sparseExample** collection มาใช้ทดสอบ
2. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
3. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **avatar_url 1**
4. กด option 
5. **เลื่อนลงมาด้านล่าง** จะเห็นตัวเลือก Sparse index ให้กดเลือก
6. กดสร้าง
7. กลับมาที่ tab **documents** ให้ทำการเลือก Query 
8. ในช่อง Query ให้ใส่รายละเอียดคำสั่งดังนี้ และกดปุ่ม **Find**

```js
{ avatar_url: { $exists: true } }
```

9. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (มีการใช้ Sparse index) ให้กดเปิดดูรายละเอียดใน execution stage ว่าค่า `isSparse` เป็น `true`
   2. Document examined
   3. Document returned
   4. Execution Time