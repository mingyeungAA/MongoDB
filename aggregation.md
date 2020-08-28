## 📄aggregation

## 💬pipeline

- colleciton이 각 stage를 거치면서 document 처리 및 집계
- 일부 처리는 shard에 대응 (각 shard에서 처리)
- **⭐pipeline** : 이전 단계의 연산 결과를 다음 단계에서 사용
- **⭐stage 순서 중요!!**
- `db.collection.aggregate(pipeline, options)`

<br>

<img src="https://postfiles.pstatic.net/MjAyMDA4MjlfMTE2/MDAxNTk4NjMwMTQ3NzA3.z7t3o_RVKHWW-eL12p6iidKfW1wGuKyCgFkbVPdEMGwg.YUcl15hq3gCo8fO4kE5ZTLWjoZIaRPA9FRpH797YbzMg.PNG.mingyeung/image.png?type=w966" style="zoom:50%;" />

<br>

```
db.orders.aggregate([
   { $match: { status: "A" } },
   { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
])
```

> first stage : `$match` stage는 status필드에서 "A"와 같은 document를 찾는다.

> second stage : `$group` stage에서는 각각의 유일한 cust_id의 수를 세서 묶어준다.(grouping)

<br>

<br>

#### ❕`db.collection.aggregate(pipeline, options)`

[reference](https://docs.mongodb.com/manual/reference/method/db.collection.aggregate/#db.collection.aggregate)

| Parameter | type     | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| pipeline  | array    | A sequence of data aggregation operations or stages. |
| options   | document | Optional.                                            |

<br>

ex)

```javascript
db.score.aggregate(
  //score collection 에서
  {$match:{"test":"midterm"}},
  //test가 midterm 인 document들을 뽑고,
  {$project:{"kor":1}},
  //kor만 출력시켜서, {_id:"..", kor:""}
  {$group:{"_id":"test","average":{"$avg":"$kor"}}
  //집계해서 {_id:"test", average:n}으로 출력한다.
)
```

<br>

---

<br>

| SQL      | NoSQL    |
| -------- | -------- |
| WHERE    | $match   |
| GROUP BY | $group   |
| HAVING   | $match   |
| SELECT   | $project |
| ORDER BY | $sort    |
| LIMIT    | $limit   |
| SUM      | $sum     |
| COUNT    | $sum     |

<br>

<br>

---

## 💬map-reduce⭐

- aggregation framework가 처리하지 못하는 **복잡한 집계** 작업에 사용
- **javascript function을 사용**하여 복잡한 작업 처리
- shard에 대응 -> 분산처리가능

<br>

<img src="https://postfiles.pstatic.net/MjAyMDA4MjlfNTMg/MDAxNTk4NjMzNDQzOTY0.EyguTZJOLej5W3I5D8deJGRWS4AXmZC9SEQ0cnaxWLUg.zd57yZr98pewS0ZrCsF15x8WUWKktmlQUPgEDK32Tk4g.PNG.mingyeung/image.png?type=w966" style="zoom:50%;" />

- 순서  (query -> map -> reduce -> out)
  - map : data mapping (grouping)
  - reduce : 집계 연산 실행
  - query : 입력될 document
  - out : collection or document 출력

[reference](https://docs.mongodb.com/manual/core/map-reduce/)

<br>