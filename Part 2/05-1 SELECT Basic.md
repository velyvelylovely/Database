## [SELECT로 데이터 조회하기](https://www.youtube.com/watch?v=dTBwgWMUguE&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=6)

데이터베이스에서 원하는 데이터를 추출하는 방법을 알아보겠습니다. 예를 들어, ID가 9인 임직원의 이름과 직급을 알고 싶다면 어떻게 해야 할까요? 이때 사용하는 것이 바로 `SELECT`문입니다.

`SELECT`문은 데이터베이스의 테이블에서 원하는 데이터를 조회하는데 사용됩니다. 이때 `WHERE` 절에서 조건을 명시하는 것을 선택 조건(Selection condition)이라고 합니다. 선택 조건은 employee 테이블에서 어떤 튜플을 선택할지를 알려줍니다.

그리고 내가 알고 싶은 필드(속성, Attribute)를 지정해서 해당 필드에 대응하는 값을 가져오는 것을 투영 속성(Projection Attribute)이라고 합니다. 

따라서 `SELECT`로 데이터를 조회할 때는 선택 조건을 통해 데이터를 필터링하고, 그 중에서 투영 속성에 의해 지정된 필드에 해당하는 값만을 가져옵니다.

### SELECT 문 사용 방법

`SELECT`문의 기본 구조는 아래와 같습니다.

```sql
SELECT attribute(s)
FROM table(s)
    [WHERE condition(s)]
;
```

실제 적용을 위해 project 테이블과 employee 테이블에서 데이터를 조회하는 예시를 보겠습니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/9f075d41-9049-4872-baaa-3697bab069f5)

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

## AS

`AS`는 SQL에서 별칭(alias)을 붙일 때 사용하는 키워드입니다. 이를 통해 테이블이나 속성(Attribute)의 이름을 다르게 표현할 수 있습니다. 특히 복잡한 쿼리를 작성할 때나, 결과의 컬럼 이름을 명확하게 표현하고 싶을 때 유용하게 사용됩니다.

```sql
SELECT E.id AS leader_id, E.name AS leader_name, position 
FROM project AS P, employee AS E
	WHERE P.id = 2002 and P.leader_id = E.id
;
```

위의 예시에서는 `AS` 키워드를 사용해 `E.id`를 `leader_id`, `E.name`을 `leader_name`으로 표시합니다. 그리고 `AS`는 생략 가능합니다. 따라서 아래와 같이 쿼리를 작성할 수도 있습니다.

```sql
SELECT E.id leader_id, E.name leader_name, position 
FROM project P, employee E
	WHERE P.id = 2002 and P.leader_id = E.id
;
```

**쿼리 실행 결과**

| leader_id | leader_name | position |
| --- | --- | --- |
| 13 | JISUNG | PO |

## DISTINCT

`DISTINCT`는 `SELECT` 결과에서 중복되는 행(Tuples)을 제거할 때 사용하는 키워드입니다. 즉, 고유한 결과만을 얻고 싶을 때 사용합니다.

![image](https://github.com/velyvelylovely/Database/assets/98696925/92dc252f-1ac6-4ff2-af7a-a12d8ab8f0b8)

```sql
SELECT DISTINCT P.id, P.name
FROM employee AS E, works_on AS W, project AS P
	WHERE E.position = 'DSGN' and
		E.id = W.empl_id and W.proj_id = P.id
;
```

위의 쿼리는 'DSGN' 직급의 직원이 참여한 프로젝트의 ID와 이름을 중복 없이 조회하는 쿼리입니다.

**쿼리 실행 결과**

| id | name |
| --- | --- |
| 2002 | 확장성 있게 백엔드 리팩토링 |
| 2003 | 홈페이지 UI 개선 |
| ~~2003~~ | ~~홈페이지 UI 개선~~ |

## LIKE

`LIKE`는 문자열 패턴 매칭에 사용되는 키워드입니다. 즉, 특정 패턴을 가진 문자열을 찾고 싶을 때 사용할 수 있습니다. 

이때, `%`는 0개 이상의 임의의 문자를 의미하며, `_`는 하나의 문자를 의미합니다. 또한, `\`는 뒤따라오는 특수문자를 일반 문자로 해석하게 하는 이스케이프 문자입니다.

예를 들어, 이름이 'N'으로 시작하거나 끝나는 직원의 이름을 찾고 싶다면 아래와 같이 쿼리를 작성할 수 있습니다.

```sql
SELECT name
FROM employee 
	WHERE name LIKE 'N%' or name LIKE '%N'
;
```

**쿼리 실행 결과**

| name |
| --- |
| BROW`N` |
| JOH`N` |
| `N`ICOLE |

또는, 이름에 'NG'가 포함된 직원을 찾고 싶다면 아래와 같이 작성할 수 있습니다.

```sql
SELECT name
FROM employee 
	WHERE name LIKE '%NG%'
;
```

**쿼리 실행 결과**

| name |
| --- |
| DI`NG`YO |
| JISU`NG` |

또는, 이름이 'J'로 시작하고 길이가 4인 직원을 찾고 싶다면 아래와 같이 작성할 수 있습니다.

```sql
SELECT name FROM employee WHERE name LIKE 'J___'
;
```

**쿼리 실행 결과**

| name |
| --- |
| `J`ANE |
| `J`OHN |

### escape 문자와 함께 LIKE 사용하기

`LIKE` 키워드를 사용할 때, 특정 문자열이 `%`로 시작하거나 `_`로 끝나는 경우를 찾고 싶을 때에는 어떻게 해야 할까요? 이때 사용하는 것이 escape 문자입니다. 

예를 들어, 프로젝트 이름이 `%`로 시작하거나 `_`로 끝나는 경우를 찾고 싶다면, 아래와 같이 쿼리를 작성할 수 있습니다.

```sql
SELECT name FROM project WHERE name LIKE '\%%' or name LIKE '%\_'
;
```

위의 쿼리에서 백슬래시(`\`)는 escape 문자로, 뒤따라오는 특수 문자를 일반 문자로 해석하게 합니다. 

### LIKE 정리

| 항목 | 설명 |
| --- | --- |
| LIKE | 문자열 패턴 매칭에 사용 |
| reserved character | % : 0개 이상의 임의의 문자를 의미, _ : 하나의 문자를 의미 |
| escape character | \ : 예약 문자를 escape시켜서 문자 본연의 문자로 사용하고 싶을 때 사용 |

## * (asterisk)

`*`(asterisk)는 SQL에서 모든 속성(Attribute)를 선택할 때 사용하는 기호입니다. 즉, 선택된 튜플의 모든 속성을 보여주고 싶을 때 사용합니다.

```sql
SELECT * FROM employee WHERE id = 9
;
```

위의 쿼리는 `employee` 테이블에서 `id`가 9인 직원의 모든 정보를 조회하는 쿼리입니다.

## SELECT without WHERE

`WHERE`절 없이 `SELECT`문을 사용하면, 해당 테이블에 저장된 모든 데이터를 가져옵니다. 즉, 테이블의 모든 행(Tuple)을 반환합니다. 이는 특정 조건으로 데이터를 필터링하지 않고, 전체 데이터를 조회하고 싶을 때 유용합니다.

## 주의사항

데이터베이스에서 `SELECT`문을 이용해 데이터를 조회할 때, 특정 조건을 설정해서 데이터를 찾는 경우가 많습니다. 이때, 이 조건에 해당하는 속성(Attribute)에 인덱스(Index)가 설정되어 있다면, 데이터 검색 속도가 훨씬 빨라집니다. 

인덱스는 책의 색인과 같은 역할을 하여, 데이터베이스에서 데이터를 빠르게 찾을 수 있도록 도와줍니다. 따라서, 인덱스가 없는 속성에 대해 데이터를 조회하면, 전체 데이터를 검색해야 하므로 데이터 양이 많을수록 조회 속도가 느려집니다.

예를 들어, `employee` 테이블에서 `position`이 'dev_back'인 직원을 찾는다면, `position` 속성에 인덱스가 설정되어 있어야 효율적으로 데이터를 조회할 수 있습니다.

```sql
SELECT * FROM employee WHERE position = 'dev_back';
```

이 쿼리는 `position`이 'dev_back'인 모든 직원의 정보를 조회하는 쿼리입니다. 이때 `position` 속성에 인덱스가 있다면, 해당 조건에 맞는 데이터를 빠르게 찾아낼 수 있습니다.

