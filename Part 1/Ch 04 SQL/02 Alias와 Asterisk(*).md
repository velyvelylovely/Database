## Alias

SQL에서 Alias는 테이블 이름이나 컬럼 이름을 단순화하거나 가독성을 높이기 위해 사용합니다. Alias은 테이블이나 컬럼의 이름을 임시로 바꾸어, 쿼리문을 더욱 간결하고 이해하기 쉽게 만들 수 있습니다.

테이블에 대한 Alias은 테이블명 바로 뒤에 위치하며, 컬럼에 대한 Alias은 컬럼 바로 뒤에 위치합니다. 이 때 `AS` 키워드를 사용하여 Alias을 지정할 수 있습니다. 하지만 `AS` 키워드는 선택사항이므로 생략할 수도 있습니다.

```sql
SELECT e.name AS employee_name, e.position AS job_title
FROM employees AS e
;
```

위의 예시에서 'employees' 테이블에 'e'라는 Alias을 지정하고, 'name' 컬럼에 'employee_name', 'position' 컬럼에 'job_title'이라는 Alias을 지정했습니다.

## Asterisk(*)

SQL에서 `*`는 '모든 컬럼'을 의미합니다. 특정 테이블의 모든 컬럼을 선택하려면 `*`를 사용할 수 있습니다.

```sql
SELECT *
FROM employees
;
```

위의 예시에서는 'employees' 테이블의 모든 컬럼을 선택하는 SELECT 문을 작성했습니다. 이렇게 `*`를 사용하면 테이블의 모든 데이터를 간편하게 조회할 수 있습니다.
