# Compound Indexes

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. ทดสอบ Compound Index

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{
  released: { $gte: ISODate("2000-01-01T00:00:00Z") },
  rated: "G"
}
```
3. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังที่มีการเข้าฉายตั้งแต่ปี 2000 ขึ้นไป และเป็นหนังที่เหมาะสำหรับทุกเพศทุกวัย
4. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time
5. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
6.  กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
7. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **released** และเลือกเป็น **ascending** (1)
8. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{
  released: { $gte: ISODate("2000-01-01T00:00:00Z") },
  rated: "G"
}
```

9. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
10. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time 
11. กลับมาที่ tab **Indexes** ทำการลบ index **released** ออก
12. สร้าาง index แบบ Compound ด้วย field **released** และ **rated** และเลือกเป็น **ascending** (1) ตามลำดับ
13. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{
  released: { $gte: ISODate("2000-01-01T00:00:00Z") },
  rated: "G"
}
```

14. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
15. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time 

## Index Prefixes

- ใน Compound indexes ตัว Mongo จะใช้แค่ Prefixes index เท่านั้น
- เช่น ตั้ง compound index เป็น `{ city: 1, district: 1, soi: 1}`
- ค่า. Prefix คือ 
	- `{ city: 1 }`
	- `{ city: 1, district: 1 }`

### ทดสอบการทำงานของ Index Prefixes

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{
  released: { $gte: ISODate("2000-01-01T00:00:00Z") },
}
```

3. กดปุ่ม Explain สังเกตว่า MongoDB เรายังใช้ compound index ได้อยู่
4. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง และกดปุ่ม Find 
   
```js
{
  rated: "G"
}
```

5. กดปุ่ม Explain สังเกตว่า MongoDB เราไม่ได้ใช้ compound index แล้ว

- สังเกตว่าถ้าเราระบุใช้ index ตัวสุดท้ายที่อยู่ใน compound index ทาง MongoDB จะไม่สนใจการใช้ compound index นั้น แต่ถ้าเราระบุใช้ index ตัวแรกที่อยู่ใน compound index ทาง MongoDB จะใช้ compound index นั้น
- ดังนั้นการใช้ index ควรระบุเฉพาะ prefix หรือทั้ง compound ไปเลย
- index prefix ใช้กับการทำ compound index ที่มีการเรียงลำดับของ field ที่เราต้องการใช้ index ในการ query และเรียงลำดับของ field ใน index ตามลำดับที่เราต้องการใช้ใน query นั้นๆ


    