# List privilege in User Role

รัน mongod

```bash
mkdir -p role1/db
mongod --auth --dbpath role1/db --logpath role1/db/mongod.log --port 26000
```

ใช้ mongo shell สร้าง user 

```bash
mongo --port 26000
use admin
db.createUser( { user: 'pon', pwd: 'pass', roles: [{role: 'userAdminAnyDatabase', db:'admin' ]})
```

Authenticate user

```bash
db.authen('pon','pass')
```

เรียกดู privilege 

```bash
var role = db.getRole('userAdminAnyDatabase', {showPrivileges: true})

role

// ดูจำนวน privilege
role.privileges.length

// ไล่ดูทีละ privilege
role.priviledes[0]
```
