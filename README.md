# MongoDB for DBA Workshop

## โดย [Nextflow.in.th](https://www.nextflow.in.th)

## Setup guideline

- [Setup](setup.md)

## Presentation

- [Download MongoDB for DBA](https://nextflowth-my.sharepoint.com/:b:/g/personal/teerasej_nextflowth_onmicrosoft_com/EeqKc8r0cxJJrcWgFKF_VO0BC9Zr5yvg3gT8BDYo-SKUgw?e=8as9dR)
- [Download Indexes](https://nextflowth-my.sharepoint.com/:b:/g/personal/teerasej_nextflowth_onmicrosoft_com/Eb_b9M49RTpAjcxJ3YpQiSMBAWSBI9GOB4l6DUe1wbP98w?e=BuobDH)
- [Download Security](https://nextflowth-my.sharepoint.com/:b:/g/personal/teerasej_nextflowth_onmicrosoft_com/EZRbXBaShZtCn-2iIZ5CLmEBPjA6ClPjiujqRS96alR_Ug?e=s6MRej)
- [Download Administration](https://nextflowth-my.sharepoint.com/:b:/g/personal/teerasej_nextflowth_onmicrosoft_com/ERzUeVp1rdlOqmERmBrStJQBJZETPLDKdvqvCuPOVBSQDA?e=oMLS40)

## Mongo Atlas

1. [สมัคร และทดลองสร้าง Cluster บน Mongo Atlas](contents/atlas-create-cluster-free.md)
2. [ฝึกเชื่อมต่อ Cluster ด้วย Mongo Compass](contents/compass-connect-example-cluster.md)

## MongoDB Shell

1. [ฝึกเชื่อมต่อ Cluster บน Atlas ด้วย Mongo Shell และใช้คำสั่งพื้นฐาน](contents/mongo-shell-connect-example-cluster)
2. [รัน MongoDB ด้วย Shell](contents/connect-mongodb-with-shell.md) ([คำอธิบายเพิ่มเติม](contents/mongod-command.md))
3. [ฝึกเชื่อมต่อ Local Cluster ด้วย Mongo Compass](contents/compass-connect-localhost-cluster.md)

## MongoDB Command

- [เรื่อง Mongo Document](contents/mongod-document.md)
- [SQL compare to MongoDB](https://docs.mongodb.com/manual/reference/sql-comparison/)

1. [โหลดข้อมูล ด้วยคำสั่ง `mongoimport`](contents/mongo-import.md)
2. [Insert Operation](contents/mongo-operation-insert.md)
3. [Read Operation](contents/mongo-operation-read.md)
4. [Update Operation](contents/mongo-operation-update.md)
5. [Remove Operation](contents/mongo-operation-remove.md)

### Q&A

- [ค้นหาแบบ case-insensitive](https://stackoverflow.com/questions/1863399/mongodb-is-it-possible-to-make-a-case-insensitive-query)

### วิธีต่างๆ ที่ใช้แทน JOIN 

** อย่าลืมว่า MongoDB ออกแบบมาเพื่อให้ประสิทธิภาพในการอ่าน/เขียน Data จากฐานข้อมูลสู่ระดับ Application ทำงานได้เร็วที่สุด กลไก JOIN จึงไม่มีมาตั้งแต่ต้น แต่ $lookup ก็สามารถพิจารณาเอามาใช้งานในทำนองเดียวกันได้ รวมถึงแนวคิดต่างๆ ที่เอามาทดแทน JOIN ได้ครับ

- [$lookup example](https://stackoverflow.com/a/33511166)
- [สร้าง JOIN Collection](https://stackoverflow.com/a/22739813)

## Indexing 

1. [Single Field Indexes](contents/index-single-field.md)
2. [Index Sorting](contents/index-sorting.md)
3. [Index Compound](contents/index-compound.md)

## MongoD Command & Config

1. [Setup Vagrant Image Environment](contents/vagrant-image-setup.md)
2. [MongoD Command](contents/mongod-command.md)
3. [MongoD Configuration Files](contents/mongod-config-file.md)

## Security & Authentication

1. [Security: First Admin account (Localhost exception)](contents/security-localhost-exception.md)
2. [Security: Authentication method](contents/security-authentication-method.md)

## Replica Set 

1. [Setting up a Replica Set](contents/replica-set-config-file.md)
2. [# Reconfiguring a Running Replica Set](contents/replica-set-reconfig.md)

### Q&A

- [Connection String แบบต่างๆ](https://docs.mongodb.com/manual/reference/connection-string)

## Sharding

1. [Setting up a shared cluster](contents/shard-config-file.md)

## Exercise

- [Exercise in Advanced Topics for Database Administrator](contents/advanced/README.md)