# Compound Indexes with Sort

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. ทดสอบ Compound Index with sort

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่รายละเอียดคำสั่งดังนี้ และกดปุ่ม **Find**

```js
{ year: 2000 }
```
Option > Sort
```js
{ "tomatoes.viewer.meter": -1 }
```

3. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังปี 2000 ที่ sort ตาม tomatoes.viewer.meter จากมากไปน้อย
4.  กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่า Sort in memory)
   2. Document examined
   3. Document returned
   4. Execution Time
5. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
6. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
7. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **year** และ **tomatoes.viewer.meter** และเลือกเป็น **ascending** (1) และ **descending** (-1) ตามลำดับ
8. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{ year: 2000 }
```
Option > Sort
```js
{ "tomatoes.viewer.meter": -1 }
```

9. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
10. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time 
11. สังเกตว่า Sort in memory จะหายไป และจะเป็นการใช้ index ที่สร้างขึ้นมาใหม่