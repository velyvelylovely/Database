## SELECT로 데이터 조회하기

데이터베이스에서 원하는 데이터를 추출하는 방법을 알아보겠습니다. 예를 들어, ID가 9인 임직원의 이름과 직급을 알고 싶다면 어떻게 해야 할까요? 이때 사용하는 것이 바로 `SELECT`문입니다.

`SELECT`문은 데이터베이스의 테이블에서 원하는 데이터를 조회하는데 사용됩니다. 이때 `WHERE` 절에서 조건을 명시하는 것을 선택 조건(Selection condition)이라고 합니다. 선택 조건은 employee 테이블에서 어떤 튜플을 선택할지를 알려줍니다.

그리고 내가 알고 싶은 필드(속성, Attribute)를 지정해서 해당 필드에 대응하는 값을 가져오는 것을 투영 속성(Projection Attribute)이라고 합니다. 

따라서 `SELECT`로 데이터를 조회할 때는 선택 조건을 통해 데이터를 필터링하고, 그 중에서 투영 속성에 의해 지정된 필드에 해당하는 값만을 가져옵니다.

### SELECT statement

`SELECT`문의 기본 구조는 아래와 같습니다.

```sql
SELECT attribute(s)
FROM table(s)
	[WHERE condition(s)]
;
```

실제 적용을 위해 project 테이블과 employee 테이블에서 데이터를 조회하는 예시를 보겠습니다.

```sql
SELECT employee.id, employee.name, position 
FROM project, employee
	WHERE project.id = 2002 and project.leader_id = employee.id
;
```

위의 쿼리에서 `project.id = 2002`는 선택 조건(Selection Condition)이며, `project.leader_id = employee.id`는 조인 조건(Join Condition)입니다. 또한, `employee.id, employee.name, position`는 투영 속성(Projection Attribute)입니다. 

이 쿼리를 실행하면 아래와 같은 결과를 얻을 수 있습니다.

**쿼리 실행 결과**

| id | name | position  |
| --- | --- | --- |
| 13 | JISUNG | PO |

즉, 위의 쿼리는 project 테이블의 id가 2002인 프로젝트의 리더인 임직원의 id, 이름, 그리고 직급을 조회하는 쿼리입니다.
