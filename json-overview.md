# JSON

Document ของ MongoDB แสดงในรูปแบบของ JSON (JavaScript object notation) โดยใช้สัญลักษณ์ `{}` 

โดยใน document จะประกอบไปด้วย field  

```js
{ field }
```

แต่ละ field จะมีส่วนประกอบของ key และค่าที่เก็บไว้ใน key เรียกว่า value

```js
{ "key": "value" }
```

ซึ่ง value สามารถเป็น document ได้ด้วย เราเรียกว่า nested หรือ sub document

```js
{ 
	"name": {
		"first" : "Teeasej",
		"last" : "Jiraphatchandej"
	}
}
```

JSON Spec [http://www.json.org/](http://www.json.org/)
