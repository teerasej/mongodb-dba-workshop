
# สมัคร และทดลองสร้าง Cluster บน Mongo Atlas

## 1. สร้าง Atlas Cluster

- สร้าง Account [https://cloud.mongodb.com/links/registerForAtlas](https://cloud.mongodb.com/links/registerForAtlas)
- ลงชื่อเข้าใช้งาน [https://cloud.mongodb.com/user/login](https://cloud.mongodb.com/user/login)

### 2. กดสร้าง Cluster

![2019-05-07_22-07-15](https://user-images.githubusercontent.com/85179/57312227-57a30a00-7117-11e9-96ad-73010e1cfa5b.png)


1. เลือก AWS 
2. เลือก​ Region ที่มี **Free tier** ในที่นี้เราจะเลือก Singapore
3. เลือก Cluster Tier เป็น 0 (แน่นอน ฟรี)
4. ตั้งชื่อ Cluster Name เป็น `Sandbox`
5. หลังจากสร้าง Cluster เสร็จ ให้ไปที่ Setting และตั้งชื่อ **Project Name** จาก **Project 0** เป็น `M001`

## 3. ตั้งค่า Security ให้ Cluster

![2019-05-07_22-31-42](https://user-images.githubusercontent.com/85179/57312562-021b2d00-7118-11e9-9f76-2d239d6e83e7.png)


1. เลือก Project
2. เลือก Security
3. เลือก IP Whitelist
4. กดเพิ่ม IP address

กดเลือก **Connect from Anywhere** และกดยืนยัน 

**ในที่นี้เราเปิด connect from anywhere ในการอบรมเท่านั้น นะ นะ นะ**


## 4. สร้าง User

![2019-05-07_22-29-49](https://user-images.githubusercontent.com/85179/57312418-b5375680-7117-11e9-8829-f2851095a154.png)

Cluster \> MongoDB Users \> Add new user

กำหนดข้อมูลต่อไปนี้้

- Username: m001-student
- Password: m001-mongodb-basic
- User Privileges: Read and Write to any database

## 5. เชื่อมต่อไปที่ Cluster 

1. จาก Cluster Overview คลิกปุ่ม Connection 
2. เลือก Connect with Mongo Shell
3. ในที่นี้้ ถ้าใช้ MongoDB ต่ำกว่า 4.0.2 ให้ดาวน์โหลดและติดตั้ง. Mongo Shell ตามข้อ 1
4. กดเลือก connection string ตามเวอร์ชั่นของ Mongo Shell (ดูได้จากการรันคำสั่ง `mongo --version`)

นำ connection string มารันใน Cmd หรือ Terminal เช่น

```bash
mongo "mongodb://sandbox1-shard-00-00-wkmdm.mongodb.net:27017,sandbox1-shard-00-01-wkmdm.mongodb.net:27017,sandbox1-shard-00-02-wkmdm.mongodb.net:27017/test?replicaSet=Sandbox1-shard-0" --ssl --authenticationDatabase admin --username m001-student --password <PASSWORD>`
```
