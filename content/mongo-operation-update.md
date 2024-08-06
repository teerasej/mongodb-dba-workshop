# Update Operation

## UpdateOne()

- อัพเดต document แรกที่ตรงกับกรณีที่กำหนด

```js
.updateOne( {search} , { $set: {key:value} })
```

- ดูเพิ่มเติม Update Operator [https://docs.mongodb.com/manual/reference/operator/update/](https://docs.mongodb.com/manual/reference/operator/update/)

### $inc

- เพิ่มค่า `rating` เข้าไปอีก 3 จากค่าเดิม

```js
.updateOne( {search} , { $inc: {rating:3} })
```

### $push

- ใช้ในการเพิ่ม document ลงไปใน key ที่เป็น array
- ถ้าต้องการเพิ่มหลายตัวพร้อมกัน ให้ใช้ควบคู่กับ `$each`

```js
.updateOne( {search} , 
			{ $push: { 
				review: { 
					$each:[
						{ score: 1 }
					],
					[
						{ score: 4 }
					]
				}
			} 
})
```

## UpdateMany()

- อัพเดตทุก document ที่ตรงกันกรณีที่กำหนด
- จากตัวอย่าง ค่าที่กำหนดให้ key สำหรับ Operator `$unset` เป็นค่าอะไรก็ได้

```js
.updateMany( { rated: null} , { $unset: rated: "" })
```

## Upsert()

- ถ้าไม่มี document ไหนตรง mongo จะทำการสร้าง document ใหม่ให้ใน collection โดยใช้ค่าจาก `$set`

```js
.updateOne( {search} , { $set: {...} }, { upsert: true} )
```

