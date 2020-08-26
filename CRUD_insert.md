## 📄CRUD

### 💬[insert()](https://docs.mongodb.com/manual/tutorial/insert-documents/)

: Create or insert operations add new documents to a collection.

<br>

![](https://postfiles.pstatic.net/MjAyMDA4MjZfNzEg/MDAxNTk4NDM4NjU3Nzcz._O-g_3Ak-U2cRcy1U_UiqQH3bjOhCAo2jTWE-kqR1Dgg.raW-4Qtk6kD6L3w0c0YcAYbrzx0TEmySqu3w_Gzjl2cg.PNG.mingyeung/image.png?type=w966)

<br>

- **`db.collection.insertOne()`**
- **`db.collection.insertMany()`**

<br>

**`_id` (=primary key) : 명시하지 않으면 자동으로 Objectid값을 생성한다.

<br>

<br>

---

#### **❕`db.collection.insertOne()`**

: insert  a single document into a collection.

<br>

```javascript
db.inventory.insertOne(
   { item: "canvas", qty: 100, tags: ["cotton"], size: { h: 28, w: 35.5, uom: "cm" } }
)
```



<br>

---

#### **❕`db.collection.insertMany()`**

: insert multiple documents into a collection.

<br>

```javascript
db.inventory.insertMany([
   { item: "journal", qty: 25, tags: ["blank", "red"], size: { h: 14, w: 21, uom: "cm" } },
   { item: "mat", qty: 85, tags: ["gray"], size: { h: 27.9, w: 35.5, uom: "cm" } },
   { item: "mousepad", qty: 25, tags: ["gel", "blue"], size: { h: 19, w: 22.85, uom: "cm" } }
])
```

<br><br>

---

**Collection : 특별히 따로 만들겠다고 선언하지 않아도 자동으로 만들어짐

&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;&nbsp;  : If the collection does not currently exist, insert operations will create the collection.



<br>

**Atomicity (원자성) : field(key) 중복 불가!

<br>

