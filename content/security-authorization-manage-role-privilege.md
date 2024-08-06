# การจัดการ Role และ Privilege

## Update Role

Authenticate user ของเราก่อน

```bash
db.auth('pon','pass')
```

เราสามารถอัพเดต role ของ user ได้

```bash
db.updateUser('peter', { roles: [{ role: 'read', db: 'admin' }]} )
```

## Create Role

```bash
db.createRole( {role: 'internRole', privileges: [ {...} ], roles: [{ role: 'read', db:'nfmongop'}]})
```

-  Privilege เช่น `{ resource: { db: 'nfmongop', collection:'peoples'}, actions: ["update"] }`

## Grant privilege to role

```bash
db.grantPrivilegesToRole( 'role name', [ {...} ])
```

- `{ resource: { db:'', collection: '' }, actions: ['action name'] }`

 หรือจะถ่ายโอน privilege จาก role ที่มีอยู่ก่อนแล้วก็ได้

```bash
db.grantRolesToRole( 'role เป้าหมาย', [ '...' ])
```

- ชื่อ role ที่จะถ่ายทอด privilege ให้ role เป้าหมาย เชื่อ `'readWrite’`

## Revoke Privilege

```bash
db.revokePrivilegesFromRole( 'role เป้าหมาย', [ {...} ])
```

- `{ resource: { db:'', collection: '' }, actions: ['action name'] }`