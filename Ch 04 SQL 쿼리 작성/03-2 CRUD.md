## CRUD 

CRUD는 컴퓨터 프로그래밍에서 데이터를 관리하는 데 가장 기본적인 네 가지 작업으로 Create(생성), Read(읽기), Update(수정), Delete(삭제)의 첫 글자를 따서 만든 약어입니다.

CRUD를 SQL 명령어를 통해 직접 실습해 보겠습니다. 

![image](https://github.com/velyvelylovely/Database/assets/98696925/e0e707ac-82f3-4788-ab64-0ae84fa5fa75)

## CREATE(INSERT)

`CREATE(INSERT)`는 새로운 데이터를 생성하거나 추가하는 작업을 말합니다. 예를 들어, 새로운 사용자 계정을 만드는 것이 이에 해당합니다.

DataGrip 툴을 사용하여 `testdb1`을 선택하고 미리 생성해둔 `member`테이블에 아래의 쿼리를 실행합니다.

```
insert into member
(name, email, mobile_no, password, marketing_yn, register_date)
values
('apple', 'test@naver.com', '01011111111', '1234', true, now())
```

>[!NOTE]
>실행할 문장을 드래그를 하고 `Ctrl + Enter`를 하면 해당 쿼리가 실행됨

![image](https://github.com/velyvelylovely/Database/assets/98696925/d8628d62-85ff-45df-b29d-06e9d76fc701)

동일한 쿼리를 두 번 실행한 후 결과를 확인해보면, 동일한 열이 두 번 중복으로 표시됩니다.

