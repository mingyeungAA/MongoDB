## 📄MongoDB

### 💬NoSQL 이란?

- Non Relational

- 고정되지 않은 테이블 스키마 (=스키마가 고정되어있지 않다. =쿼리가 없다.)

   -> 필요할때 마다 필드를 추가/제거 가능 (=개발 속도 향상)

- 데이터 간의 관계를 정의하지 않는 데이터베이스

- 분산형 구조 (**대용량 데이터** 저장 용이)

   -> sharding 지원 (클라스터 데이터 상호 복제)

<br><br>

---

#### mongo shell (interactive javascript interface)

- **javascript interpreter** 사용

- js program, library, function 활용가능

  **interactive : REPL (Read Eval Print Loop 대화형 프로그래밍 언어)

<br>

---

### 💬Database

- 독립적인 하나의 권한을 가진다.
- 각각의 db는 분리된 파일로 저장된다.
- 예약된 db name
  - admin : root db 
  - local : 복제되지 않는 db(특정서버에만 저장하는 collection에 사용)
  - config : shard 정보 저장

<br>

<br>

---

### 💬Collection (=table)

- document들의 group ( =rdbms의 table 역할 = 값이 저장될 모양)

- schema를 가지지 않는다. (document들의 field가 각각 다를 수 있다.)

  **schema : 메타데이터





<br>

<br>

### ⭐Document(=데이터)⭐

- data recode를 [BSON](http://bsonspec.org/) (⭐Binary JSON)으로 저장 (-> 가벼움)

- field(key) 중복 불가

- 대소문자 구별

- {field : value} 형태

  ![](https://postfiles.pstatic.net/MjAyMDA4MjZfNTkg/MDAxNTk4NDM3MDEyMjM4.HgYjVJ3SPV-_diaqf2HoDswI79187ErRAdqNfwMUG38g.C-najnhLzf3u-mMMgILPWLdMbCY8_O9cye_nqP-70wwg.PNG.mingyeung/fieldvalue.png?type=w966)

<br>

---

#### 💬명령어

show dbs  &nbsp; &nbsp;  전체 database 목록

db &nbsp; &nbsp;&nbsp; 현재 database 확인

use dbname &nbsp; &nbsp; 해당 database로 변경

show collections &nbsp; &nbsp; 현재 database의 collection 목록

<br>

<br>