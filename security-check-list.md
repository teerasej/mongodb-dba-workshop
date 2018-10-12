# Security Checklist

## Enable Access Control and Enforce Authentication

- client ทุกตัวต้อง authen เข้ามาใช้งาน
- เปิดการทำงานของ Authentication บน MongoDB Server ทุกตัว

## Configure Role-based Access Control

- สร้าง user account ให้กับผู้ใช้แต่ละคน หลีกเลี่ยงการใช้บัญชีร่วม
- กำหนด user privilege ที่เหมาะสมกับผู้ใช้คนนั้น อย่าให้สิทธิ์ root พร่ำเพรื่อ
- จัดกลุ่ม Privilege ที่ใช้บ่อยๆ เป็น Role เพื่อกำหนดให้กับ User 

## Encrypt Communication

- Transport Encryption
	- `mongod --sslMode requireSSL`
- Encryption at rest
	- `mongod --enableEncryption`
- Sign & Rotate Encryption Key 
- Protect MongoDB data using file-system permission
	- `chmod 700 data/db`
		- permission to only current user
		- no permission for owner group or anyone else

## Limit Network Exposure

- ตั้งค่า firewall เพื่อควบคุมการเข้าถึง MongoDB system
	- จำกัดการเข้าถึงจาก app มาที่ port และระบบที่เจาะจง
- ใช้ VPN/VPC สร้าง secure tunnel 
- ใช้ `bind_ip`
	- `mongod --bind_ip:127.0.0.1`

## Audit System Activity

- Track change to DB config
	- `mongod --auditDestination file`
- Track change to data

## Run mongoDB as dedicated user

- MongoDB ไม่ควรรันด้วย root user 

## Run MongoDB ด้วย Secure Configuration Options 

- Disable HTTP Status Interface
	- `mongod --httpinterface`
	- deprecated and disabled by default
- Disable REST API
	- `mongod --rest`
	- deprecated and disabled by default
- Disable server-side scripting
	- ปกติ mongodb จะรองรับ javascript scripting เช่น `mapReduce()`, `group()`, `$where`
	- ถ้าไม่ใช้ ก็ปิดซะ ด้วย `mongod --noscripting`

## ดู mongoDB Security Reference 

- [https://www.mongodb.com/collateral/mongodb-security-architecture]

