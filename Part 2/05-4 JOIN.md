## [JOIN](https://www.youtube.com/watch?v=E-khvKjjVv4&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=10)

- JOIN은 두 개 이상의 테이블에 있는 데이터를 한 번에 조회하는 기능을 말합니다.
- JOIN에는 여러 가지 종류가 존재합니다.

## Implict JOIN vs Explict JOIN

### Implict JOIN

- FROM절에는 테이블들을 나열하고, WHERE절에 조인 조건을 명시하는 방식을 말합니다.
- 이 방식은 old-style join syntax라고도 불립니다.
- WHERE절에 선택 조건과 조인 조건이 함께 있어 가독성이 떨어질 수 있습니다.
- 복잡한 JOIN 쿼리를 작성하다 보면 실수로 잘못된 쿼리를 작성할 가능성이 높아집니다.

```sql
SELECT D.name
FROM employee AS E, department AS D
WHERE E.id = 1 AND E.dept_id = D.id
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/83b16152-6b06-40fc-b76c-aead49568b93)

### Explict JOIN

- FROM절에 JOIN 키워드와 함께 조인할 테이블들을 명시하는 방식을 말합니다.
- 이 방식에서는 FROM절에서 ON 다음에 조인 조건이 명시됩니다.
- 가독성이 좋고, 복잡한 JOIN 쿼리를 작성하는 과정에서 실수할 가능성이 적습니다.

```sql
SELECT D.name
FROM employee AS E JOIN department AS D ON E.dept_id = D.id
WHERE E.id = 1
;
```

## Inner JOIN vs Outer JOIN

### Inner JOIN

- 두 테이블에서 조인 조건을 만족하는 튜플들로 결과 테이블을 생성하는 JOIN 방식을 말합니다.
- 사용법 : `FROM table1 [INNER] JOIN table2 ON join_condition`
- 조인 조건에서 사용 가능한 연산자는 =, <, >, ≠ 등 다양한 비교 연산자가 있습니다.
- 조인 조건에서 NULL 값을 가지는 튜플은 결과 테이블에 포함되지 않습니다. 이는 조인 조건이 반드시 TRUE여야만 튜플을 가져오는데, UNKNOWN은 TRUE가 아니기 때문입니다. 따라서 조인 조건이 TRUE인 경우에만 매칭되는 튜플을 가져옵니다.

```sql
SELECT *
FROM employee E INNER JOIN department D ON E.dept_id = D.id
;
```

### Outer JOIN

- 두 테이블에서 조인 조건을 만족하지 않는 튜플들도 결과 테이블에 포함하는 JOIN 방식을 말합니다.
- `FROM table1 LEFT [OUTER] JOIN table2 ON join_condition` : 왼쪽 테이블의 모든 튜플을 누락하지 않고 표현합니다.
- `FROM table1 RIGHT [OUTER] JOIN table2 ON join_condition` : 오른쪽 테이블의 모든 튜플을 누락하지 않고 표현합니다.
- `FROM table1 FULL [OUTER] JOIN table2 ON join_condition` : 모든 테이블의 매칭되지 않는 결과도 누락하지 않고 표현합니다.(MySQL에서는 지원하지 않습니다.)
- 조인 조건에서 사용 가능한 연산자는 =, <, >, ≠ 등 다양한 비교 연산자가 있습니다.

## Equi JOIN

- 조인 조건에서 등호(=)를 사용하는 조인 방식을 말합니다.

### Equi JOIN에 대한 두 가지 관점

- 내부 조인, 외부 조인에 상관없이 등호를 사용한 조인을 Equi JOIN으로 보는 경우
- 내부 조인에 한정하여 등호를 사용한 경우에만 Equi JOIN으로 보는 경우

## USING

- 두 테이블이 동등 조인을 할 때, 조인하는 속성의 이름이 같다면, USING을 이용해 간편하게 표현할 수 있습니다.
- 이때 같은 이름의 속성은 결과 테이블에서 한 번만 표시됩니다.
- `FROM table1 [INNER] JOIN table2 USING (Attribute(s))`
- `FROM table1 LEFT [OUTER] JOIN table2 USING (Attribute(s))`
- `FROM table1 RIGHT [OUTER] JOIN table2 USING (Attribute(s))`
- `FROM table1 FULL [OUTER] JOIN table2 USING (Attribute(s))`

```sql
SELECT *
FROM employee E INNER JOIN department D ON E.dept_id = D.dept_id
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/ecf4fd7d-60b6-45d2-afe5-84cf6dc7a9b5)

```sql
SELECT *
FROM employee E INNER JOIN department D USING (dept_id)
;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/7dd043ef-78f6-473e-9d11-09fbb9f1664c)

## Natural JOIN

- 두 테이블에서 같은 이름을 가진 모든 속성 쌍에 대해 Equi JOIN을 수행하는 방식을 말합니다.
- 조인 조건을 따로 명시하지 않습니다. 
- `FROM table1 NATURAL [INNER] JOIN table2`
- `FROM table1 NATURAL LEFT [OUTER] JOIN table2`
- `FROM table1 NATURAL RIGHT [OUTER] JOIN table2`
- `FROM table1 NATURAL FULL [OUTER] JOIN table2`

```sql
SELECT * 
FROM employee E NATURAL INNER JOIN department D;
```

## Cross JOIN

- 두 테이블의 튜플 쌍으로 만들 수 있는 모든 조합을 결과 테이블로 반환합니다. 이는 두 테이블의 카르테시안 곱을 반환하는 것과 같습니다.
- 조인 조건이 없습니다.
- Implicit Cross JOIN : `FROM table1, table2`
- Explict Cross JOIN : `FROM table1 CROSS JOIN table2`

```sql
SELECT *
FROM employee CROSS JOIN department;
```

![image](https://github.com/velyvelylovely/Database/assets/98696925/e9c7c774-cb24-4d4d-af1d-4ab53a3abdce)

![image](https://github.com/velyvelylovely/Database/assets/98696925/8e604ec3-6efa-4996-a956-aae2b1a731d6)

### Cross JOIN @ MySQL

- MySQL에서는 크로스 조인(Cross JOIN), 내부 조인(Inner JOIN), 그리고 단순히 JOIN이 동일하게 작동합니다.
- 크로스 조인에 ON 또는 USING을 함께 사용하면 내부 조인으로 작동합니다.
- 반대로, 내부 조인이나 JOIN이 ON 또는 USING 없이 사용되면 크로스 조인으로 작동합니다.

## Self JOIN

- 테이블이 자기 자신과 조인하는 경우를 말합니다.
