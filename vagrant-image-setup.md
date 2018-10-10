
# Vagrant Environment

1. ดาวน์โหลด zip ไฟล์ 
2. แตก zip ไฟล์
3. เปิด terminal หรือ command prompt ไปที่โฟลเดอร์ที่แตก zip file
4. รันคำสั่ง `vagrant up --provision`
5. รอโหลดให้เสร็จสมบูรณ์ (ใช้เวลานานนะ)
6. รันคำสั่ง `vagrant ssh` เพื่อเชื่อมต่อไปที่ image
7. รันคำสั่ง `validate_box` เพื่อเช็ค pass code ว่าเป็น `6445a3f8b6f1cc5873cf1ac94194903444602708d4eb189d42b6e65ca594d80d`