# Partial Indexes

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. ทดสอบ Partial Index

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่คำสั่งดังนี้ และกดปุ่ม **Find**

```js
{
  "year": { "$gte": 1900 }
}
```
3. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังที่มีปีเข้าฉายตั้งแต่ปี 1900 ขึ้นไป
4. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan
   2. Document examined
   3. Document returned
   4. Execution Time
5. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
6.  กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
7. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **year** และเลือกเป็น **ascending** (1)
8. กดเปิด option และเลือก partial expression และใส่ด้านล่างลงไป
9. ใส่ค่าดังนี้

```js
{
  "year": { "$gte": 1900 }
}
```

10. กดสร้าง index
11. กลับมาที่ tab **documents** ให้ทำการกดปุ่ม reset เพื่อล้างค่า Query ที่เคยใส่ไว้ และกดปุ่ม find อีกครั้ง
12. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่าเป็น Collscan)
   2. Document examined
   3. Document returned
   4. Execution Time
13. กลับมาที่ tab documents ให้ทำการเลือก Query ใหม่อีกครั้ง

```js
{
  rated: "G"
}
```
12. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่าเป็น Collscan)
   2. Document examined
   3. Document returned
   4. Execution Time
13. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{
  "year": { "$gte": 1900 }
}
```
14. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่าเป็น IXSCAN แล้ว')
   2. Document examined
   3. Document returned
   4. Execution Time
