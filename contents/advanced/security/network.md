
# Network Security 

## A. การเพิ่ม IP บน MongoDB Atlas Cluster

> ส่วนนี้จะเป็นการเพิ่ม IP Address ใดๆ ให้เข้าถึง MongoDB Atlas Cluster ของเราได้ 

1. เลือกโปรเจค และ Cluster ที่ต้องการเพิ่ม IP ใน MongoDB Atlas
2. จากเมนูด้านซ้าย คลิกที่ `Security` > Network Access
3. จะเห็นส่วนของ Network Access แสดงขึ้นมา
4. คลิกที่ปุ่ม `Add IP Address`
   <img width="1065" alt="2024-08-15_21-46-07" src="https://github.com/user-attachments/assets/00d5f3f7-14da-460e-8c62-2d5190f92018">
5. กดปุ่ม `Allow Access from Anywhere` หรือ `Add Current IP Address` หรือ `Add IP Address`
6. กดปุ่ม `Confirm` เพื่อยืนยันการเพิ่ม IP Address
   <img width="856" alt="2024-08-15_21-45-40" src="https://github.com/user-attachments/assets/48b58b0a-fcf2-4b92-a000-48b162875ce6">

7. เรียบร้อยแล้วตรวจเช็ค IP Address ที่เพิ่มเข้ามาในรายการ