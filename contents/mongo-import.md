# โหลดข้อมูล ด้วยคำสั่ง `mongoimport`

1. รัน Mongo Daemon [ดูการรันได้ที่นี่](connect-mongodb-with-shell.md)
2. [ดาวน์โหลด zip ไฟล์จากที่นี่](https://www.dropbox.com/s/xslq536dkofqey5/nfmongop2.zip?dl=0) และแตก zip ไฟล์
3. เปิด Command Prompt หรือ Terminal มาที่โฟลเดอร์ ที่มีไฟล์ json
4. รันคำสั่ง 

```bash
mongoimport --db nfmongop --collection people --file people.json
```

