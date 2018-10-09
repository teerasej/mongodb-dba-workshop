# Remove Operation

เราสามารถแก้ไข collection โดยการลบ document ที่ต้องการออกได้ด้วยคำสั่งด้านล่าง

```js
.remove( <query> )
```

และถ้าต้องการ เราสามารถใส่ option เพื่อให้ลบเพียงแค่ 1 document 

```js
.remove( <query> , { justOne: true } )
```
