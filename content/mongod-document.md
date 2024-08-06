# MongoDB Documents

- มี Schema ได้
- แต่จะไร้รูปแบบ Schema ก็ได้
- ใน Storage Layer ตัว MongoDB แปลง JSON เป็น BSON และแปลง BSON กลับเป็น JSON ในระดับ Application 

## Limitation

- 1 Document จำกัดที่ 16 MB
- การพยายาม insert หรือ update document ที่ทำให้ขนาดเกินพิกัด จะทำให้ error