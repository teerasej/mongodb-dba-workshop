# Logging Basic

ดู log component

```bash
mongo admin --host 192.168.103.100:27000 -u m103-admin -p m103-pass --eval '
  db.getLogComponents()
'
```

ปรับ logging level

```bash
mongo admin --host 192.168.103.100:27000 -u m103-admin -p m103-pass --eval '
  db.setLogLevel(0, "index")
'
```

ดู log file:

```bash
tail -f /data/db/mongod.log
```

ทดลองอัพเดต document:

```bash
mongo admin --host 192.168.103.100:27000 -u m103-admin -p m103-pass --eval '
  db.products.update( { "sku" : 6902667 }, { $set : { "salePrice" : 39.99} } )
'
```

