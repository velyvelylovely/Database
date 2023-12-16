## DBMS 내장 함수

DBMS 내장 함수는 DBMS가 기본적으로 제공하는 함수들로, 이들은 각종 연산이나 변환, 그리고 NULL 값 처리 등에 사용됩니다. 이 함수들은 크게 단일행 함수와 다중행 함수로 나눌 수 있습니다.

단일행 함수는 입력값으로 단일행 값이 들어가고, 다중행 함수는 여러 행의 값이 입력으로 들어갑니다. 이때 다중행 함수에는 집계 함수나 그룹 함수 등이 포함됩니다.

또한, 이들 함수는 처리하는 데이터의 유형에 따라 문자형 함수, 숫자형 함수, 날짜형 함수, 변환형 함수, NULL 관련 함수로 나눌 수 있습니다.

이제 실제 사용 예시를 보겠습니다.

```sql
select member_type, user_id, password, name
  ,
  case 
    when Length (password) > 2 then concat (substring (password, 1, 2), '**')
    else " 
  end as password_mask
from member;
```

이 코드는 `member` 테이블에서 `member_type`, `user_id`, `password`, `name` 칼럼을 조회하며, password의 길이가 2보다 크면 앞의 두 글자만 보여주고 나머지는 '**'로 마스킹하는 쿼리입니다.

여기서 사용된 `Length`, `concat`, `substring` 함수는 모두 문자형 함수이며, `case`는 조건에 따른 결과를 반환하는 제어문입니다. 

`Length (password)`는 password의 문자열 길이를 반환하고, `concat (substring (password, 1, 2), '**')`는 password의 첫 두 글자와 '**'를 연결한 문자열을 반환합니다. `case`문은 password의 길이가 2보다 길면 앞서 설명한 작업을 수행하고, 그렇지 않으면 빈 문자열을 반환합니다. 

이처럼 DBMS 내장 함수를 활용하면 다양한 조건에 맞게 데이터를 처리하고 변환하는 작업을 수행할 수 있습니다.
