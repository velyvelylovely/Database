## [SQL에서 NULL의 의미](https://www.youtube.com/watch?v=y_7rOoOodCY&list=PLcXyemr8ZeoREWGhhZi5FZs6cvymjIBVe&index=8)

SQL에서 NULL은 특별한 의미를 지니며, 주로 아래 세 가지 상황에서 사용됩니다.

- **알 수 없음(unknown)**: 특정 필드의 정보가 없거나 알아낼 수 없는 상황을 표현합니다. 예를 들어, 직원의 생년월일 정보가 없는 경우 'birth_date' 필드에 NULL이 할당될 수 있습니다.
- **사용 불가능(unavailable) 또는 숨김(withheld)**: 정보가 사용할 수 없거나, 보안 등의 이유로 공개되지 않아야 하는 경우를 표현합니다.
- **해당사항 없음(not applicable)**: 특정 필드가 적용될 수 없는 상황을 표현합니다. 예시로, 미혼인 직원에게는 '배우자의 이름'이라는 필드가 적용되지 않으므로, 이 경우 해당 필드에 NULL이 지정될 수 있습니다.

NULL값과 비교하기 위해 SQL 쿼리를 작성할 때는, `=` 대신 `IS NULL`이나 `IS NOT NULL`을 사용해야 합니다. 

즉, `SELECT id FROM employee WHERE birth_date = NULL` 대신 `SELECT id FROM employee WHERE birth_date IS NULL`로 표현해야 하는 것입니다.

## NULL과 Three-Valued Logic의 관계

SQL에서 NULL을 비교 연산에 사용하면 그 결과는 'UNKNOWN'이라는 상태가 됩니다. 이 'UNKNOWN' 상태는 "참일 수도 있고, 거짓일 수도 있다"는 의미를 내포하며, 이는 바로 SQL의 Three-Valued Logic 기반에서 파생된 것입니다.

Three-Valued Logic은 기존의 이진 논리(Boolean Logic)를 확장한 개념으로, 비교나 논리 연산의 결과가 '참(TRUE)' 또는 '거짓(FALSE)' 이외에도 '알 수 없음(UNKNOWN)'이라는 세 번째 상태를 포함하고 있습니다. 따라서 SQL의 비교/논리 연산은 '참', '거짓', '알 수 없음' 이라는 세 가지 결과를 가질 수 있습니다. 이 세 가지 결과값은 SQL 쿼리의 결과에 중요한 영향을 미치므로, NULL과 Three-Valued Logic에 대한 정확한 이해는 SQL을 효율적으로 활용하는 데 필수적입니다.

### NULL의 비교 연산 결과

![image](https://github.com/velyvelylovely/Database/assets/98696925/d54ee145-ac52-4a21-bae0-ff42f011b765)

### UNKNOWN의 논리 연산 결과

![image](https://github.com/velyvelylovely/Database/assets/98696925/42006c17-82d7-44e7-9687-cfc4022ee983)

## WHERE절의 조건식 이해하기

- WHERE절에 위치한 조건식(Condition)의 결과가 TRUE인 튜플만 선택됩니다. 
- 즉, 조건식의 결과가 FALSE나 UNKNOWN인 경우, 해당 튜플은 선택되지 않습니다.

## NOT IN 사용 시 주의 사항

'v NOT IN(v1, v2, v3)'는 'v ≠ v1 AND v ≠ v2 AND v ≠ v3'와 동일한 의미를 지닙니다.

그런데 만약 v1, v2, v3 중 하나의 값이 NULL인 경우에는 어떻게 될까요?

| NOT IN 사용 예제 | 결과 |
| --- | --- |
| 3 NOT IN (1, 2, 4) | TRUE |
| 3 NOT IN (1, 2, 3) | FALSE |
| 3 NOT IN (1, 3, NULL) | FALSE |
| 3 NOT IN (1, 2, NULL) | UNKNOWN |

위의 예시에서 '3 NOT IN (1, 2, NULL)'의 결과가 UNKNOWN인 이유는 NULL이 '알 수 없음'을 의미하기 때문입니다. 따라서 3과 NULL을 비교했을 때 그 결과는 '알 수 없음(UNKNOWN)'이 됩니다.

이와 같이 UNKNOWN 결과를 반환하지 않도록 하려면, NULL 값을 다룰 때 'IS NOT NULL'을 사용해야 합니다. 이를 통해 NULL 값이 포함된 경우를 효과적으로 처리할 수 있습니다.
