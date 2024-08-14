# Single Field Indexes with Sub-document


## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)

### 1. ทดสอบ Single Fields Index แบบ sub-document

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{ "tomatoes.viewer.meter": { "$gt": 90 } }
```
3. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังที่มีคะแนนจากผู้ชมมากกว่า 90
4. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time
5. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
6. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
7. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **tomatoes.viewer.meter** และเลือกเป็น **ascending** (1)
8. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{ "tomatoes.viewer.meter": { "$gt": 90 } }
```

9. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
10. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time 
11. กลับมาที่ tab **Documents** และรัน Query ดังนี้

```js
{
  "tomatoes.viewer.meter": { "$gt": 75 },
  "genres": "Drama"
}
```
12. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังที่มีคะแนนจากผู้ชมมากกว่า 75 และเป็นหนังแนว Drama
13. 10. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (เป็น index scan ก่อนที่จะ filter โดยใช้ genres)
   2. Document examined
   3. Document returned
   4. Execution Time 
14. กลับไปที่ tab **indexes** และลบ index **tomatoes.viewer.meter** ออก

