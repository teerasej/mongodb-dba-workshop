

# ทดสอบ Route

## ดาวน์โหลด และติดตั้ง POSTMan 

- [ดาวน์โหลดตัวติดตั้ง POSTMan](https://www.getpostman.com/)

## ใช้งาน POSTMan ในการจำลองการส่ง Request เข้า Web API

![2020-01-27_22-36-30](https://user-images.githubusercontent.com/85179/73188618-ba30b000-4155-11ea-8d11-e8033b8a8ae6.png)

1. ปุ่มสร้าง Request ใหม่
2. รายการแสดงข้อมูลของ Request
3. เลือกประเภท HTTP Method
4. ใส่ URL ที่ต้องการส่ง Request ไป
5. ปุ่มกดเพื่อส่ง Request
6. ส่วนประกอบของ Request ที่สามารถปรับแต่งได้ เช่นการกำหนด JSON ลงไปใน Request สำหรับ HTTP Post
7. ผลลัพธ์ที่ได้กลับมาจาก Web API

## URL ที่ใช้ในการทดสอบ

สามารถใช้ Collection ที่โค้ชพลสร้างไว้ แล้ว import เข้ามาใช้งานได้ ดาวน์โหลดจากที่นี่

- **GET** http://localhost:3000/
- **GET** http://localhost:3000/people
- **POST** http://localhost:3000/people

กำหนดค่า
Body -> Raw (JSON)

```json
{
	"first_name": "John",
	"last_name": "Constantine"
}
```

- **PUT** http://localhost:3000/people

กำหนดค่า
Body -> Raw (JSON)

```json
{
    "_id": "",
	"first_name":"Thanos"
}
```

- **DELETE** http://localhost:3000/people

กำหนดค่า
Body -> Raw (JSON)

```json
{
    "_id": ""
}
```

