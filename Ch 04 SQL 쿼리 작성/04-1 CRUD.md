## CRUD 

CRUD는 컴퓨터 프로그래밍에서 데이터를 관리하는 데 가장 기본적인 네 가지 작업으로 Create(생성), Read(읽기), Update(수정), Delete(삭제)의 첫 글자를 따서 만든 약어입니다.

CRUD를 SQL 명령어를 통해 직접 실습해 보겠습니다. 

![image](https://github.com/velyvelylovely/Database/assets/98696925/e0e707ac-82f3-4788-ab64-0ae84fa5fa75)

## INSERT

`INSERT`는 데이터베이스에 새로운 데이터를 생성하거나 추가하는 작업을 말합니다. 예를 들어, 새로운 사용자 계정을 만드는 것이 이에 해당합니다.

DataGrip 툴을 사용하여 이전에 생성한 `testdb1` 데이터베이스를 선택하고 `member` 테이블에 아래의 `INSERT` 문을 실행하여 새로운 데이터를 생성해 보겠습니다.

```mysql
insert into member
(name, email, mobile_no, password, marketing_yn, register_date)
values
('apple', 'test@naver.com', '01011111111', '1234', true, now())
;
```

>[!NOTE]
>실행할 문장을 드래그를 하고 `Ctrl + Enter`키를 누르면 해당 쿼리가 실행됨

![image](https://github.com/velyvelylovely/Database/assets/98696925/d8628d62-85ff-45df-b29d-06e9d76fc701)

동일한 `INSERT` 쿼리를 두 번 실행하면, 동일한 데이터가 테이블에 두 번 중복으로 입력됩니다.

데이터를 데이터베이스에 삽입할 때, 각 행은 고유하게 식별되어야 합니다. 이를 통해 해당 데이터에 대해 다양한 조작을 수행할 수 있습니다. 

이러한 목적으로 주로 `PK(Primary Key)`라는 개념을 사용합니다. `PK`는 테이블 내의 각 레코드를 고유하게 식별하는 열(또는 열의 조합)입니다. `PK`는 중복 값이 허용되지 않으며 NULL 값을 가질 수 없습니다.

또한 `FK(Foreign Key)`라고도 하는 외래 키 개념이 있습니다. `FK`는 테이블 간의 관계를 정의하는 데 사용됩니다.

### PK(Primary Key) 설정

예를 들어, `email`이 `PK`로 지정된 경우, `email` 열 내에서 중복된 이메일 주소를 포함하지 않아야 하며, 모든 행은 유일한 이메일 주소를 가져야 합니다. 이를 통해 데이터베이스에서 각 레코드를 식별하고 조회, 수정 또는 삭제하는 데 사용할 수 있습니다. 

>[!NOTE]
>`PK`를 지정함으로써 데이터 무결성을 유지하고 데이터 중복을 방지함

아래 SQL 명령어를 통해 `member` 테이블에서 `email` 컬럼을 `PK`로 지정해 보겠습니다.

```mysql
ALTER TABLE member
ADD CONSTRAINT pk_member PRIMARY KEY (email)
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/10d7c7d4-496b-4c5d-8704-d63f29d47f72)

그러나 현재 테이블에 입력된 데이터는 같은 이메일 주소가 중복되기 때문에 `PK`를 지정할 수 없으므로 에러가 발생합니다.

그래서 기존의 `member` 테이블을 삭제하고, `PK`를 지정한 새로운 테이블을 생성해 보겠습니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/e648cac7-2fbb-497e-8f94-97f2ca78d883)

테이블 삭제는 매우 주의해야하므로 `drop table member;` 명령어를 실행하기 전에 신중하게 검토해야 합니다. 이후 `create table member`를 사용하여 새 테이블을 생성하고, `select * from member;`로 테이블을 조회하면 아무 내용도 포함되지 않는 것을 확인할 수 있습니다.

이제 `email`을 `PK`로 지정하고 테이블을 조회하면, `email`에 `PK`를 나타내는 기호가 표시됩니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/a85a6fb0-7036-4e5b-be06-ea3c39340cf2)

![image](https://github.com/velyvelylovely/Database/assets/98696925/3715fa29-d1d0-4f20-b7ed-8b27022260cd)

동일한 데이터를 두 번 이상 삽입하려고 하면 이메일이 중복되기 때문에 **Multiple primary key defined** 오류가 발생합니다. `PK`는 중복 값을 허용하지 않기 때문입니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/3b254fd4-9184-4ca9-b52f-d45dbec65499)

### PK(Primary Key) 제거

`member` 테이블의 `PK`를 제거하려면 아래 명령어를 사용합니다. `PK`는 제거되지만 데이터는 그대로 남아 있습니다.

```mysql
alter table member drop primary key
;
```

## UPDATE

`UPDATE`는 데이터베이스의 기존 레코드를 수정하는 데 사용되는 명령어입니다. 이 명령어를 사용하면 테이블에서 하나 이상의 컬럼 값을 변경할 수 있습니다.

먼저 `member`테이블에 데이터를 추가하고 다음 명령어를 실행하여 `marketing_yn` 를 `false`로 `UPDATE`해보겠습니다.

```mysql
update member
set
    marketing_yn = false
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/1cbd21c7-7ccb-407b-9ecb-55829f1c35d5)

그럼 **Unsafe query: 'Update' statement without 'where' updates all table rows at once** 라는 메세지가 뜨는데 이 내용은 조건이 없는 업데이트는 모든 데이터를 변경하기 때문에 위험하다는 메세지 입니다. 

Execute 를 클릭하면 전체 `marketing_yn`가 `false`로 바뀌는 것을 확인할 수 있습니다. 

![image](https://github.com/velyvelylovely/Database/assets/98696925/2dfb7c90-36d4-40c5-a34a-7ce11c51e370)

### WHERE 조건

`UPDATE` 문을 사용할 때에는 조건을 지정할 수 있습니다. `WHERE` 절을 사용하여 `test@naver.com` 이메일 주소를 가진 사용자의 정보만 변경할 수 있습니다.

```mysql
update member
set
    marketing_yn = false
    , register_date = now()
    , password = '1111'
where email = 'test@naver.com'
;
```

>[!NOTE]
>`INSERT` 문과는 달리, `UPDATE`와 `DELETE` 문에서는 조건을 지정할 수 있음

## DELETE

DELETE 문은 데이터베이스의 데이터를 삭제하는 데 사용되는 명령어입니다. 특정 조건을 만족하는 튜플을 선택하여 해당 튜플을 데이터베이스에서 삭제합니다. 

```sql
delete
from 테이블명
where 삭제조건
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/7ec942e2-1fe0-4fd2-a69f-7568b918aa10)

## SELECT 

SELECT 문은 데이터베이스에서 원하는 데이터를 조회하거나 추출할 때 사용하는 구문입니다.

```sql
SELECT 출력 대상 컬럼명, 출력 대상 컬럼명 ...
FROM 출력 대상 컬럼들이 있는 테이블명
WHERE 조건
;
```




