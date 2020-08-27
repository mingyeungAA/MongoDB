## 📄CRUD

### 💬[delete](https://docs.mongodb.com/manual/tutorial/remove-documents/)

: **Delete** operations remove documents from a collection.

: delete operations target a single collection.

<br>

<img src="https://postfiles.pstatic.net/MjAyMDA4MjhfMTc4/MDAxNTk4NTQ1NjYxMjU3.zc2AeGha9WOy5r_6UhXLDTxx79avZMPjSVZAOPDPRdMg.70vRm90Hb0vdKXxgzuAmedvjus0migjJIrjnV2Wb9OUg.PNG.mingyeung/image.png?type=w966" style="zoom:50%;" />

<br>

- **`db.collection.deleteOne(filter, options)`**
- **`db.collection.deleteMany(filter, options)`**

<br>

*filter : 수정할 document를 find(). &nbsp; [query selector](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors)

*options : 추가적인 기능 (writeConcern,collection,...)

<br>

---

#### **❕`db.collection.deleteOne(filter, options)`**

: To delete at most a single document that matches a specified filter

: 특정 조건에 맞는 하나의 document만 삭제

<br>

```db.inventory.updateOne(
db.inventory.deleteOne( { status: "D" } )
```

<br>

##### 👉returns

- deleteCount : 삭제된 document들의 수를 리턴

- acknowledged(boolean) : true이면 write concern을 사용한다. 

  ***write* *concern* : mongoDB가 client의 요청으로 데이터를 기록할때, 해당요청에 대한 response

  ​                               를 어느 시점에 주느냐에 대한 동작 방식. **데이터 일관성** 유지 가능

<br>

---

#### **❕`db.collection.deleteMany(filter, options)`**

: To delete all documents from a collection, pass an empty filter document {}

: document들 전체 삭제 or 특정 조건에 맞는 document들 삭제

<br>

``` 
db.inventory.deleteMany({})
```

```
db.inventory.deleteMany({ status : "A" })
```

<br>

##### 👉returns

- deleteCount : 삭제된 document들의 수를 리턴

- acknowledged(boolean) : true이면 write concern을 사용한다. 

  ***write* *concern* : mongoDB가 client의 요청으로 데이터를 기록할때, 해당요청에 대한 response

  ​                               를 어느 시점에 주느냐에 대한 동작 방식. **데이터 일관성** 유지 가능

<br>

<br>