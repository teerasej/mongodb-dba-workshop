# Single Field Indexes


## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)

### 1. ทดสอบการค้นหาข้อมูลโดยไม่ใช้ Index

1. จาก database **sample_mflix** ให้เลือก **users** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{ name:"Ned Stark" }
```
3. ตรวจสอบผลลัพธ์ที่ได้ 
4. กดปุ่ม Explain และสังเกตค่าที่ได้
   1. Plan ที่ได้คือ **COLLSCAN** หมายความว่า mongodb ไล่เทียบเช็คค่าตามเงื่อนไขทุก document ใน collection
   2. **185 documents examined** คือ mongodb ไล่เช็คทุก document ใน collection
   3. **1 documents returned** คือ mongodb ได้เจอ 1 document ที่ตรงกับเงื่อนไข
   4. **Execution​ Time** คือเวลาที่ใช้ในการค้นหา

### 2. ทดสอบการค้นหาด้วยการใช้ Single Field Indexes

1. จาก database **sample_mflix** ให้เลือก **users** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{ email :"sean_bean@gameofthron.es" }
```
3. ตรวจสอบผลลัพธ์ที่ได้ 
4. กดปุ่ม Explain และสังเกตค่าที่ได้
   1. Plan ที่ได้คือ **IXSCAN** -> **FETCH** หมายความว่า mongodb นำเงื่อนไขที่ตรงกับ index มาเทียบก่อน และส่ง document ที่ตรงออกไปจาก collection

### 3. ทดสอบการใช้งาน Single Field Indexes ในการค้นหาข้อมูลของ comments collection

1. จาก database **sample_mflix** ให้เลือก **comments** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{email: "mercedes_tyler@fakegmail.com" }
```
3. ตรวจสอบผลลัพธ์ที่ได้ 
4. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time
5. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
6. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
7. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **email** และเลือกเป็น **ascending** (1)
8. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{email: "mercedes_tyler@fakegmail.com" }
```

9. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
10. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time 
11. กลับไปที่ tab **indexes** และลบ index **email** ออก
