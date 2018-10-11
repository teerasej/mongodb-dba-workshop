# คำสั่งค้นหา pid ของ process mongod ในกรณีที่ต้องการเคลียร์ทิ้ง

```bash
ps -ef | grep mongod
```

เมื่อทราบ pid แล้วใช้คำสั่ง

```bash
kill <pid>
```
