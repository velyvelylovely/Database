## [Subquery](https://www.youtube.com/watch?v=lwmwlA2WhFc&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=6)

서브쿼리는 쿼리 내부에 포함된 또 다른 쿼리를 의미합니다. 이는 복잡한 데이터 요청을 처리하는 데 유용하게 사용됩니다. 서브쿼리는 `SELECT`, `INSERT`, `UPDATE`, `DELETE` 문 등에 포함될 수 있으며, 서브쿼리를 포함하는 바깥 쿼리를 외부 쿼리라고 부릅니다. 서브쿼리는 괄호 `()`로 감싸게 됩니다.

예를 들어, 아래의 쿼리는 `employee` 테이블에서 ID가 14인 직원보다 생일이 빠른 직원의 id, name, birth_date를 조회하는 쿼리입니다.

```sql
SELECT id, name, birth_date FROM employee
WHERE birth_date < (
		SELECT birth_date FROM employee WHERE id = 14
		);
```

## IN

`IN`은 특정 값이 괄호 안의 값들 중 하나와 일치하는지를 확인하는 데 사용됩니다. 괄호 안의 값들은 직접 명시할 수도 있고, 서브쿼리의 결과일 수도 있습니다. `NOT IN`은 `IN`의 반대 개념으로, 괄호 안의 어떠한 값과도 일치하지 않는 경우 `TRUE`를 반환합니다.

바깥쪽 쿼리에서 참조하는 속성(Attribute)은 해당 속성이 사용된 쿼리를 포함하여 그 쿼리의 바깥쪽에 있는 모든 쿼리 중에서, 해당 속성 이름을 가지는 가장 가까운 테이블을 참조합니다.

```sql
SELECT id, name
FROM employee,
	(
		SELECT DISTINCT empl_id
		FROM works_on
		WHERE empl_id != 5 AND proj_id IN (
			SELECT proj_id
			FROM works_on
			WHERE empl_id = 5
			)
		) AS DSTNCT_E
WHERE id = DSTNCT_E.empl_id;
```

## EXISTS

서브쿼리가 바깥쪽 쿼리의 속성을 참조할 때, 이를 상호 연관된 서브쿼리라고 합니다. `EXISTS`는 서브쿼리의 결과가 최소 하나의 행(row)라도 존재하는 경우 `TRUE`를 반환합니다.

```sql
SELECT P.id, P.name
FROM project P
WHERE EXISTS (
	SELECT *
	FROM works_on W
	WHERE W.proj_id = P.id AND W.empl_id IN (7, 12)
	);
```

## NOT EXISTS

`NOT EXISTS`는 `EXISTS`의 반대 개념으로, 서브쿼리의 결과가 단 하나의 행도 없는 경우 `TRUE`를 반환합니다.

```sql
SELECT D.id, D.name
FROM department AS D
WHERE NOT EXISTS (
	SELECT *
	FROM employee E
	WHERE E.dept_id = D.id AND E.birth_date >= "2000-01-01"
 );
```

## ANY

`ANY`는 서브쿼리가 반환하는 결과 중에서 단 하나라도 특정 조건을 만족하는 경우 `TRUE`를 반환하는 키워드입니다. `ANY`는 다른 비교 연산자와 함께 사용되며, `SOME` 키워드와 같은 기능을 합니다.

아래의 쿼리는 각 부서의 리더가 그 부서의 최대 급여보다 적은 급여를 받는 직원 중에 하나라도 있다면, 그 리더의 id, 이름, 급여, 그리고 부서의 최대 급여를 조회하는 쿼리입니다.

```sql
SELECT E.id, E.name, E.salary,
	(
		SELECT max(salary)
		FROM employee
		WHERE dept_id = E.dept_id
	) AS dept_max_salary
FROM department D, employee E
WHERE D.leader_id = E.id AND E.salary < ANY (
		SELECT salary
		FROM employee
		WHERE id <> D.leader_id AND dept_id = E.dept_id
	);
```

## ALL

`ALL` 키워드는 서브쿼리가 반환하는 모든 결과가 특정 조건을 만족하는 경우에 `TRUE`를 반환합니다. `ALL` 역시 다른 비교 연산자와 함께 사용됩니다.

아래의 쿼리는 ID가 13인 직원이 참여하지 않은 모든 프로젝트에 참여한 직원의 id, 이름, 직위를 조회하는 쿼리입니다.

```sql
SELECT DISTINCT E.id, E.name, E.position
FROM employee E, works_on W
WHERE E.id = W.empl_id AND W.proj_id <> ALL (
	SELECT proj_id
	FROM works_on
	WHERE empl_id = 13
	);
```

## 참고 사항

- 성능 비교: `IN`과 `EXISTS`의 성능 차이는 RDBMS의 종류와 버전에 따라 다릅니다. 하지만 최근의 RDBMS는 많은 개선이 이루어져 `IN`과 `EXISTS`의 성능 차이가 거의 없다고 알려져 있습니다.
- 위의 내용은 MySQL 기준으로 작성되었습니다. 다른 RDBMS의 SQL 문법은 조금씩 다를 수 있습니다. 따라서 실제 환경에서는 사용하는 RDBMS의 문법에 맞추어 쿼리를 작성해야 합니다.
