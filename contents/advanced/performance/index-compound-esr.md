# Compound Indexes Optimization with ESR

## Exercise

### 0. เตรียมระบบ (ถ้ายังไม่ได้ทำ)

[สร้าง mongodb cluster บน mongoDB Atlas และเชื่อมต่อกับ Mongo Cluster](../prepare/README.md)


### 1. ทดสอบ Compound Index with sort

1. จาก database **sample_mflix** ให้เลือก **movies** collection มาใช้ทดสอบ
2. ในช่อง Query ให้ใส่รายละเอียดคำสั่งดังนี้ และกดปุ่ม **Find**

```js
{
  rated: "G",
  released: { $gte: ISODate("2000-01-01T00:00:00Z") }
}
```
Option > Sort
```js
{ "title": 1 }
```

1. ตรวจสอบผลลัพธ์ที่ได้ จะเป็นหนังที่มีการจัดอันดับเป็น G และมีการเข้าฉายตั้งแต่ปี 2000 ขึ้นไป และเรียงตามชื่อหนัง
2.  กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่า Sort in memory และ Collscan)
   2. Document examined
   3. Document returned
   4. Execution Time
3. กดปิดหน้าต่าง explain และกลับมาที่หน้าจอเดิม
4. กด tab **Indexes** และสังเกตว่ามี index อะไรบ้าง
5. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยใช้ field **rated** และ **released** และ **title**
6. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{
  rated: "G",
  released: { $gte: ISODate("2000-01-01T00:00:00Z") }
}
```
Option > Sort
```js
{ "title": 1 }
```

7. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
8. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่า Sort in memory ยังอยู่)
   2. Document examined
   3. Document returned
   4. Execution Time 
9. กด tab **Indexes** 
10. กดปุ่ม **Create Index** และสร้าง index ใหม่ โดยเราจะทำการเปลี่ยนการเรียงลำดับของ index ใหม่ที่สร้างขึ้นมา โดยให้เรียงตาม field **rated** และ **title** และ **released** ตามเทคนิคของ ESR (Equality, Sort, Range)
11. กลับมาที่ tab **documents** ให้ทำการเลือก Query ใหม่อีกครั้ง
   
```js
{
  rated: "G",
  released: { $gte: ISODate("2000-01-01T00:00:00Z") }
}
```
Option > Sort
```js
{ "title": 1 }
```

7. กดปุ่ม find และตรวจสอบผลลัพธ์ที่ได้ 
8. กดปุ่ม Explain และสังเกตค่าการทำงานต่อไปนี้
   1. Plan (สังเกตว่า Sort in memory หายไปแล้ว)
   2. Document examined
   3. Document returned
   4. Execution Time 