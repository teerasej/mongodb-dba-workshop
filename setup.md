
# Setup your machine 


ให้ทำตามครบทุกขั้นตอนเพื่อให้แน่ใจว่า ระบบและซอฟต์แวร์สามารถทำงานได้อย่างไม่มีปัญหา **และควรทำล่วงหน้าก่อนวันอบรมสักอย่างน้อย 4-5 วัน เพราะถ้าพบว่าเครื่องของตัวเองถูก block หรือจำกัดสิทธิ์ จะได้ทำเรื่องกับฝ่าย Security หรือ Admin เพื่อดำเนินการให้สามารถติดตั้งและใช้งานได้ตามปกติ**

## ⚠️ ข้อควรระวัง เรื่องการใช้เครื่องคอมขององค์กร มาใช้ในการอบรม

- **แนะนำว่าสำหรับองค์กรที่มีการ block การทำงานผ่านอินเตอร์เน็ต เช่นการ block port หรือ certificate ให้เตรียม Account สำหรับเชื่อมต่ออินเตอร์เน็ตวงนอกให้ผู้เข้าอบรมได้เลย**
- การอบรมจะมีการรันคำสั่งผ่าน โปรแกรม Command Prompt หรือ Terminal และมีโปรเซสที่ทำการสร้างและแก้ไขไฟล์ที่อยู่บนระบบปฏิบัติการ (เช่น NodeJS process) ให้แน่ใจว่าระบบปฏิบัติการไม่ได้มีการบล๊อคการทำงาน และสามารถทำงานได้อย่างไม่มีปัญหา
- ระหว่างการอบรม จะมีการเชื่อมต่ออินเตอร์เน็ต และมีการดาวน์โหลดโค้ด รวมถึงติดตั้ง, setup, และ install โปรแกรมเพิ่มเติม **ควรให้แน่ใจว่าคอมพิวเตอร์ทีี่ใช้ไม่มีการปิดกั้นการทำงานดังกล่าว**

> ⚠️⚠️⚠️ หากทางผู้ดูแลระบบไม่ได้มีการอำนวยความสะดวกในการผ่อนปรนตามสถานการณ์ด้านบน ทางผู้เข้าอบรมอาจจะไม่สามารถใช้คอมพิวเตอร์นั้นเรียนรู้ หรือทำ workshop บางส่วนได้ จึงขอแจ้งมาเพื่อทราบครับ

## 1. สำหรับ Computer ที่ใช้ในการทำงาน

ทำการดาวน์โหลดตัวติดตั้ง และดำเนินการติดตั้งให้เรียบร้อย

สำหรับคนที่ใช้ Mac สามารถติดตั้งผ่าน Homebrew ได้นะครับ 

1. MongoDB Community Edition 
   1. สำหรับ Windows ([Download](https://www.mongodb.com/try/download/community))
   2. สำหรับ MacOS สามารถ[ติดตั้งผ่าน Homebrew ได้](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-os-x/) 
2. MongoDB Shell ([Download](https://www.mongodb.com/try/download/shell))
3. MongoDB Compass ([Download](https://www.mongodb.com/try/download/compass))
4. MongoDB Command Line Database Tools [Download](https://www.mongodb.com/try/download/database-tools)
5. Git Client ([Download](http://git-scm.com/download/) | [คลิปแนะนำการติดตั้ง](https://www.youtube.com/watch?v=fPOoIZbDKmE))
6. Visual Studio Code ([Download](https://code.visualstudio.com/))
   - เสร็จแล้วติดตั้งส่วนเสริม 
     1. [MongoDB Extension](https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode)
7. Web Browser สามารถเลือกระหว่าง 2 อย่างนี้ 
   1. Google Chrome ([Download](https://www.google.com/chrome/))
   2. Microsoft Edge ([Download](https://www.microsoft.com/en-us/edge/download))

## 2. สมัคร Account ที่ควรมี

- [สมัคร Github Account](https://github.com/signup) ให้เรียบร้อย
- [สมัคร MongoDB Atlas Account](https://www.mongodb.com/cloud/atlas/register) ให้เรียบร้อย
