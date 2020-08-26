## 📄CRUD

### 💬[find()](https://docs.mongodb.com/manual/reference/method/db.collection.find/#db.collection.find)

: **Read** operations retrieves documents from a collection.

: You can specify query filters or criteria that identify the documents to return.

: returns a cursor

<br>

<img src="https://postfiles.pstatic.net/MjAyMDA4MjZfMTQ4/MDAxNTk4NDM5MTk1MDQx.-xDao5bYmQN6bpYtHyPCEwR1zh8kHWKxBjwqiKcjlw0g.MNTKWu4klyPp0okAB6GJOdPz-ni6ENXgBe-c2JWzdTgg.PNG.mingyeung/image.png?type=w966" style="zoom:50%;" />

<br>

- **`db.collection.find(query, projection)`**

<br>

---

#### **❕`db.collection.find(query, projection)`**

: Selects documents in a collection or view and return a cursor to the seleted documents.

<br>

| Parameter  | type     | Description                                                  |
| :--------- | -------- | ------------------------------------------------------------ |
| query      | document | Optional. Specifies selection filter using query operators.  |
| projection | document | Optional. Specifies the fields to return in the documents that match the query filter. |

<br>

<br>

#### 💬query 

:&nbsp; [query selector](https://docs.mongodb.com/manual/reference/operator/query/)

<br>

#### 💬projection

: determines which fields are returned in the matching documents.

<br>

```
{ <field1>: <value>, <field2>: <value> ... }
```

<br>

| Projection                  | Description                                                  |
| --------------------------- | ------------------------------------------------------------ |
| `<field> : <1 or true>`     | field안에 포함되어 있다.                                     |
| `<field> : <0 or false>`    | field안에 포함되어 있지 않다.                                |
| `"<field>.$" : <1 or true>` | $배열 projection을 사용하면, 배열에서 첫번째 요소를 리턴한다. (ex) "arrayField.$" : 1 |

<br>

---

##### ex

1. select all documents in a collection &nbsp;&nbsp;컬렉션에서 전체 찾기

   **`db.collection.find({})`** &nbsp; =&nbsp;  `SELECT * FROM COLLECTION`

   <br>

2. specify equality condition &nbsp;&nbsp;특정 한 필드 찾기

   **`db.inventory.find({status:"D"})`** &nbsp; = &nbsp; `SELECT * FROM INVENTORY WHERE status = "D"`

   <br>

3. specify conditions using query operators &nbsp;&nbsp; 쿼리명령어 사용해서 특정 필드 찾기

   **`db.inventory.find({status: {$in: ["A", "D"]}})`** &nbsp;=&nbsp; `SELECT * FROM INVENTORY WHERe status in ("A", "D")`

   <br>

4. specify and conditions

   **`db.inventory.find({status: "A", qty: {$lt: 30}})`** &nbsp; = &nbsp; `SELECT * FROM INVENTORY WHERE status = "A" AND qty < 30`

   <br>

5. specify or conditions

   : using `$or` operator

   `db.inventor.find({$or: [{status: "A"}, {qty: {$lt: 30}}]})` &nbsp;= &nbsp; `SELECT * FROM INVENTORY WHERE status = "A" OR qty < 30`

   <br>

6. specify AND as well as OR conditions

   ```
   db.inventory.find( {
        status: "A",
        $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
   } )
   ```

   =

   `SELECT * FROM INVENTORY WHERE status = "A" AND (qty < 30 OR item LIKE "p%")`



<br>

---

**cursor 

&nbsp; &nbsp; &nbsp; : A pointer to the result set of a query. Clients can iterate through a cursor to retrieve results.

<br>

<br>