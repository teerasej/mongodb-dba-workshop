# Authentication Mechanisms

## SCRAM-SHA-1

- username/password
- ใช้มาตรฐาน IEFT เพื่อป้องกัน
	- **Eavesdropping** การดักอ่านข้อมูลระหว่างทาง โดยไม่ส่ง password จริงไปกับ package
	- **Replay** hacker ปลอม client response ส่งกลับให้ server ป้องกันโดยการสร้าง unique message ในการ authenticate แต่ละครั้ง
	- **Database Compromise** hacker เข้ามาอ่านข้อมูลจาก memory ป้องกันโดยการใช้ salt และ hash password ก่อนจัดเก็บ
	- Malicious Server. 

## X.509 Certificate 

- แบบ Cert
- TLS 

## LDAP

- Lightweight Directory Access Protocol
- รองรับใน MongoDB Enterprise
- ใช้สำหรับ directory information
- ใช้ในระบบองค์กร อย่างเช่น email 

## Kerberos 

- MongoDB Enterprise
- ออกแบบสำหรับ Secure Authentication


## Internal Authentication Mechanism

- ใช้ในการยืนยัน Node ใน Replica Set หรือ Shard (เรียกว่า Member) ว่าตัวที่ติดต่อมาคือใคร
- แนะนำแม้แต่ใน เครือข่ายปิด (Close network) เพื่อประโยชน์ในกรณีที่ เครือข่ายอยู่ในสถานะ compromise
- รองรับ 2 ระบบ คือ
	- Keyfile (SCRAM-SHA-1)
		- แชร์รหัสผ่านเดียวกัน
		- ก๊อปปี้ไปใช้งานในแต่ละ member 
		- 6-1024 Base64 characters
		- ไม่สนใจ whitespace `"my pass" มีค่าเท่ากับ "mypass"`
	- X.509
		- Certificated-based
		- แนะนำให้สร้าง cert สำหรับ member แต่ละตัว
			- มีประโยชน์ในกรณีที่ cert ตัวใดตัวหนึ่งไม่ปลอดภัยแล้ว เราแค่ issue cert ใหม่แค่ตัวเดียว