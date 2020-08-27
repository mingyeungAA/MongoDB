## 📄CRUD

### 💬[update](https://docs.mongodb.com/manual/tutorial/update-documents/)

: **Update** operations modify existing documents in a collection.

: You can specify criteria, or filters, that idenfity the documents to update.

<br>

<img src="https://postfiles.pstatic.net/MjAyMDA4MjdfMTg5/MDAxNTk4NDU3MTcwMTY4.J13Lsyx84qAzqS_lkJFDwkvOfkHHoUIK7mZR2DCNyuAg.hZ4k75ECrAvXwxNhvjYq8HgoLN2KkRwAtpAb30Qewogg.PNG.mingyeung/image.png?type=w966" style="zoom:50%;" />

<br>

- **`db.collection.updateOne(filter, update, options)`**
- **`db.collection.updateMany(filter, update, options)`**
- **`db.collection.replaceOne(filter, update, options)`**

<br>

*filter : 수정할 document를 find(). &nbsp; [query selector](https://docs.mongodb.com/manual/reference/operator/query/#query-selectors)

*update : [update operator](https://docs.mongodb.com/manual/reference/operator/update/#id1) or aggregation pipeline

*options : 추가적인 기능 (upsert, writeConcern,...)

<br>

---

#### **❕`db.collection.updateOne(filter, update, options)`**

: update a single document

: document의 <span style="color:red">**field**</span> 수정

<br>

```db.inventory.updateOne(
db.inventory.updateOne(
   { item: "paper" },
   {
     $set: { "size.uom": "cm", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```

> `$set`을 사용하여 size.uom 필드를 cm로 변경하고, status를 "p"로 변경했다.
>
> `$currentDate`를 사용해 lastModified 필드를 현재 날짜값으로 변경했다.

<br>

##### 👉returns

- matchedCount : 매칭되는 document의 수를 리턴

- modifiedCount : 수정된 document의 수를 리턴

- upsertedId : upserted된 document의 _id를 리턴한다.

- acknowledged(boolean) : true이면 write concern을 사용한다. 

  ***write* *concern* : mongoDB가 client의 요청으로 데이터를 기록할때, 해당요청에 대한 response

  ​                               를 어느 시점에 주느냐에 대한 동작 방식. **데이터 일관성** 유지 가능

<br>

---

#### **❕`db.collection.updateMany(filter, update, options)`**

: update multiple document

: document의 <span style="color:red">**field**</span>수정

<br>

```
db.inventory.updateMany(
   { "qty": { $lt: 50 } },
   {
     $set: { "size.uom": "in", status: "P" },
     $currentDate: { lastModified: true }
   }
)
```

> "qty"가 50보다 작은 것들을 모두 아래의 조건으로 수정할거다.
>
> `$set`을 사용하여 size.uom필드를 "in"으로 변경하고, status필드를 "p"로 변경했다.
>
> `$currentDate`를 사용해 lastModified필드를 현재 날짜 값으로 변경했다.

<br>

##### 👉returns

- matchedCount : 매칭되는 document의 수를 리턴
- modifiedCount : 수정된 document의 수를 리턴
- upsertedId : upserted된 document의 _id를 리턴한다.
- acknowledged(boolean) : true이면 write concern을 사용한다.

<br>

---

#### **❕`db.collection.replaceOne(filter, update, options)`**

: replace a document

: _id필드 빼고 document의 모든 내용을 변경할 수 있다.

: <span style="color:red">**document**</span>를 수정

: field와 vlaue의 쌍이 반드시 맞아야 한다.

: [update operator](https://docs.mongodb.com/manual/reference/operator/update/#id1) 표현을 사용하면 안된다!

<br>

```
db.inventory.replaceOne(
   { item: "paper" },
   { item: "paper", instock: [ { warehouse: "A", qty: 60 }, { warehouse: "B", qty: 40 } ] }
)
```

<br>

<br>