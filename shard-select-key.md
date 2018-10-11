# การเลือก Shard Key 


- High Cardinality ค่า key unique มาก
	- Low Frequency ทำให้ข้อมูลกระจายไปใน Shard ได้ง่าย
	- หลีกเลี่ยง key ที่ change ได้ง่าย
	- อย่าใช้ _id_ นะ
	- เทส ใน staging ก่อน
	- Shard key จึงเป็น final