## [데이터 추가하기](https://www.youtube.com/watch?v=mgnd5JWeCK4&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=4)

데이터 추가는 `INSERT` 구문을 이용하여 수행합니다. 아래의 예시를 살펴봅시다.

```sql
INSERT INTO employee
	VALUES (1, 'MESSI', '1987-02-01', 'M', 'DEV_BACK', 100000000, null)
;
```

위의 SQL 쿼리는 'employee' 테이블에 새로운 레코드를 추가하는 명령입니다. 이 때, 레코드의 각 필드값은 괄호 안에 순서대로 나열합니다.

하지만 데이터를 추가하다 보면 몇 가지 문제에 직면할 수 있습니다. 예를 들어, 'Primary Key'가 중복되는 경우나 'Check Constraint'를 위반하는 경우에는 에러가 발생합니다.

### 중복된 'Primary Key'로 인해 에러 발생

```sql
INSERT INTO employee
	VALUES (1, 'JANE', '1996-05-05', 'F', 'DSGN', 90000000, null)
;
```

에러 메세지: `ERROR 1062 (23000): Duplicate entry ‘1’ for key ‘employee.PRIMARY’`

이 쿼리는 '1'이 이미 'employee' 테이블의 Primary Key로 사용되고 있기 때문에 새 레코드 추가를 시도하면 에러를 반환합니다.

### 'Check Constraint'가 위반되어 에러 발생

```sql
INSERT INTO employee
	VALUES (2, 'JANE', '1996-05-05', 'F', 'DSGN', 40000000, null)
;
```
에러 메세지: `ERROR 3819 (HY000): Check constraint ‘employee_chk_2’ is violated.`

이 쿼리는 'employee' 테이블에 새로운 데이터를 추가하려고 시도합니다. 하지만 이 과정에서 'employee_chk_2'라는 제약조건을 위반하였다는 에러 메시지가 발생하게 됩니다.

이런 경우, 어떤 제약조건이 위반되었는지 확인하기 위해 `SHOW CREATE TABLE employee;` 쿼리를 실행할 수 있습니다. 이 쿼리는 'employee' 테이블을 생성할 때 사용된 SQL 구문을 반환하므로, 여기서 'employee_chk_2'라는 제약조건이 어떤 것인지 확인할 수 있습니다. 이를 통해 어떤 값이 제약조건을 위반하였는지 파악하고, 이를 수정하여 에러를 해결할 수 있습니다.

### INSERT 문 사용 방법

- **테이블의 모든 속성에 대해 값을 순서대로 넣는 방법**

```sql
INSERT INTO table_name VALUES (comma-separated all values)
;
```

- **특정 속성에만 값을 넣는 방법**

```sql
INSERT INTO table_name (attributes list)
	VALUES(attributes list 순서와 동일하게 comma-separated values)
;
```

- **한 번의 명령으로 여러 튜플들을 추가하는 방법**

```sql
INSERT INTO table_name VALUES(..., ..),(..., ..),(..., ..)
;
```

## 데이터 수정하기

데이터 수정은 `UPDATE` 구문을 이용하여 수행합니다. 아래의 예시를 살펴봅시다.

```sql
UPDATE employee SET dept_id = 1003 WHERE id = 1
;
```

위의 SQL 쿼리는 'employee' 테이블에서 'id'가 1인 레코드의 'dept_id' 값을 1003으로 변경하는 명령입니다. 수정 결과를 확인하려면 다음과 같이 `SELECT` 문을 사용할 수 있습니다.

```sql
SELECT * FROM employee WHERE id = 1
;
```

또 다른 예시로, '프로젝트 ID 2003에 참여한 임직원의 연봉을 두 배로 인상하는 경우'를 살펴봅시다.

![Untitled](https://github.com/velyvelylovely/Database/assets/98696925/b45755f2-1f1f-4e35-ac24-aa80e2f1c71d)

```sql
UPDATE employee, works_on
	SET salary = salary * 2
	WHERE employee.id = works_on.empl_id and works_on.proj_id = 2003
;
```

### UPDATE 문 사용 방법

```sql
UPDATE table_name(s)
	SET attribute = value [, attribute = value, ..]
	[WHERE condition(s)]
;
```

위 명령어는 'table_name' 테이블의 'attribute' 필드를 'value'로 변경합니다. 여러 필드를 동시에 수정하려면 쉼표로 구분하여 지정할 수 있습니다. 선택적인 `WHERE` 절을 사용하여 특정 조건을 충족하는 레코드만 수정할 수 있습니다. `WHERE` 절이 없으면 테이블의 모든 레코드가 수정됩니다.

## 데이터 삭제하기

데이터 삭제는 `DELETE` 구문을 이용하여 수행합니다. 아래의 예시를 살펴봅시다.

```sql
DELETE FROM employee WHERE id = 8
;
```

위의 SQL 쿼리는 'employee' 테이블에서 'id'가 8인 레코드를 삭제하는 명령입니다.

다른 예시로, 'works_on' 테이블에서 'empl_id'가 5이고, 'proj_id'가 2001이 아닌 모든 레코드를 삭제하는 경우를 살펴봅시다.

```sql
DELETE FROM works_on WHERE empl_id = 5 and proj_id <> 2001
;
```

여기서 `<>`는 '같지 않음'을 의미합니다.

### DELETE 문 사용 방법

```sql
DELETE FROM table_name
	[WHERE condition(s)]
;
```

위 명령어는 'table_name' 테이블의 레코드를 삭제합니다. 선택적인 `WHERE` 절을 사용하여 특정 조건을 충족하는 레코드만 삭제할 수 있습니다. `WHERE` 절이 없으면 테이블의 모든 레코드가 삭제됩니다.

>[!NOTE]
> 💡 `WHERE` 절을 생략하면 모든 레코드가 삭제되므로, 데이터를 백업하고 `WHERE` 절의 조건이 올바른지 반드시 확인해야 합니다. 이는 되돌릴 수 없는 작업이므로 주의가 필요합니다.
