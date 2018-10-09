# Compound Indexes

1. Index ที่มีมากกว่า 1 field
2. ถึงแม้จะมีหลาย field แต่การใช้ก็เป็นมิติเดียว เหมือนสมุดโทรศัพท์


## Workshop 

### import ข้อมูล (ถ้ายังไม่ได้ทำ)

1. เปิด Command Prompt หรือ Terminal มาที่โฟลเดอร​์ **B-Performance**
2. รันคำสั่ง 

```bash
mongoimport --db nfmongop --collection people --file people.json
```

### ทดสอบผ่าน Compass

1. ใช้ Compass ต่อกับ MongoDB แบบ localhost
2. เลือกฐานข้อมูล **nfmongop** 
3. เลือก collection **people**
4. เลือก **Explain plan**
5. ใส่ค่า filter ดังนี้ และกดปุ่ม Explain

```json
{ last_name : "Frazier", first_name: "Jasmine" }
```

6. สังเกตตัวแสดงผล และเทียบกับการใช้ Mongo Shell

### สร้าง index ผ่าน Compass

1. เลือก tab **indexes**
2. กดปุ่ม **Create Index**
3. กรอกรายละเอียดตามนี้
	- index name: `last_name`
	- index definition: `last_name`, `1 (asc)`
4. กดสร้าง index
5. กลับมาที่ tab **Explain plan** และกด explain อีกครั้ง
6. สังเกตค่าที่เปลี่ยนไป

จะเห็นว่าค่าที่ได้คือ 1 document แต่ Examined key คือ 31 นั่นคือมีการไล่หา 31 key เพื่อจะได้เจอ document ที่ต้องการ

## สร้าง Compound index 

. เลือก tab **indexes**
2. กดปุ่ม **Create Index**
3. กรอกรายละเอียดตามนี้
	- index name: `last_name_first_name`
	- index definition: `last_name`, `1 (asc)`
	- และ `first_name `, `1 (asc)`
4. กดสร้าง index
5. กลับมาที่ tab **Explain plan** และกด explain อีกครั้ง
6. สังเกตค่าที่เปลี่ยนไป

จะเห็นว่าค่าลดเหลือแค่ 1 key examined เท่านั้น

7. ทดสอบแก้ไข filter ดังนี้

```json
{ last_name : "Frazier", first_name: { $gte: "L" } }
```

8. กด explain อีกครั้ง
9. สังเกตค่าที่เปลี่ยนไป

## Index Prefixes

- ใน Compound indexes ตัว Mongo จะใช้แค่ Prefixes index เท่านั้น
- เช่น ตั้ง compound index เป็น `{ city: 1, district: 1, soi: 1}`
- ค่า. Prefix คือ 
	- `{ city: 1 }`
	- `{ city: 1, district: 1 }`

### Workshop ด้วย Compass

1. กลับมาที่ Collection **people** 
2. เปิดส่วน **Explain plan** 
3. เปลี่ยน filter เป็น `{ last_name: "Solomon" }` และกด explain อีกครั้ง
4. สังเกตผลลัพธ์
5. เปลี่ยน filter เป็น `{ first_name: "Sonia" }` และกด explain อีกครั้ง
6. สังเกตผลลัพธ์

สังเกตว่าถ้าเราระบุใช้ index ตัวสุดท้ายที่อยู่ใน compound index ทาง MongoDB จะไม่สนใจการใช้ index 

ดังนั้นการใช้ index ควรระบุเฉพาะ prefix หรือทั้ง compound ไปเลย

### ทดลองด้วย Compass

1. ลบ index ที่ม่ีอยู่ออกทั้งหมด
2. สร้าง index แบบ 3 field 
3. ทดลองใช้ส่วน **Explain plan** กับ 
	- prefix index
	- prefix index และ field ทั่วไป
- สังเกตผลท่ี่ได้


    