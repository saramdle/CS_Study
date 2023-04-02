# Join

## 1. 조인이란?

두 개 이상의 테이블들을 연결 또는 결합하여 데이터를 출력하는 것을 조인이라고 하며 일반적으로 사용 되는 SQL문의 상당수가 조인으로 이루어져 있다.

일반적인 경우 PRIMARY KEY와  FOREIGN KEY의 값 연관에 의해 조인이 이루어지며 PK,FK관계와는 별도로 일반 칼럼끼리 조인이 이루어지는 경우도 있다.

테이블을 연결하려면, 적어도 하나의 칼럼을 서로 공유하고 있어야 하므로 이를 이용하여 데이터 검색에 활용한다.

## 2. WHY ?

왜 필요한지가 중요하다. 아래 예시 처럼 백앤드와 프론트앤드를 구분을 해서 채팅방에 회원을 넣어줘야 하는 경우가 있다고 가정하자.

왼쪽 테이블에서 숫자만 보고 누가 백앤드인지 프론트앤드인지 구분이 되지않는다. 하지만 오른쪽 테이블을 **참조**해서 보면 누가 백앤드이고 프론트앤드인지 구분이 된다.

이러한 이유 때문에 필요하다.

정리하자면…

- **서로 관계있는 데이터가 여러 테이블로 나뉘어 저장되므로 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 조인이 필요하다.**





### JOIN의 종류

---

- INNER JOIN(내부 조인)
    - CROSS JOIN
    - EQUI JOIN
    - NON-EQUI JOIN
    - NATURAL JOIN
- OUTER JOIN(외부 조인)
    - LEFT OUTER JOIN
    - RIGHT OUTER JOIN
    - FULL OUTER JOIN
- SELF JOIN
- ANTI JOIN
- SEMI JOIN

SQL 조인 쉽게 이해하기 위한 다이어 그램입니다.

![Untitled](https://file.notion.so/f/s/21f698e4-912f-4b59-9a2d-db090165b5a3/Untitled.png?id=487f155d-61cc-4eb3-bce3-9c07e65505a5&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680480713651&signature=AtQO1bl7LF8-mIPwR328nhRx4mU7dILlwTEmCNKPivU&downloadName=Untitled.png)


## 3. 내부조인(INNER JOIN)
![Untiled](https://file.notion.so/f/s/a1e84fcc-e135-44ea-8e2c-4ccfc0e191d1/Untitled.png?id=cbb7cbb0-d638-45f4-8104-e6a0cd72f074&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680490344631&signature=y32LHABB8w3NA8pX2zHkQX0cBhgjp-hDY6wVZcQ554A&downloadName=Untitled.png)
- 여러 애플리케이션에서 사용되는 가장 흔한 결합 방식이며 기본 조인 형식으로 간주됩니다.
- 내부 조인은 조인 구문에 기반한 2개의 (A,B)의 컬럼 값을 결합함으로써 새로운 결과 테이블을 생성합니다.
- 명시적 조인표현(explicit)과 암시적 조인표현(implict) 2개의 다른 조인식 구문이 있습니다.

명시적 조인 표현

> 테이블에 조인을 하나는 것을 지정하기 위해 JOIN 키워드를 사용하며 그리고 나서 다음의 예제와 같이 ON 키워드를 조인에 대한 구문을 지정하는데 사용한다.
>

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
INNER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP;
```

암시적 조인 표현

> SELECT 구문의 FROM 절에서 그것들을 분리하는 컴마를 사용해서 단순히 조인을 위한 여러 테이블을 나열하기만 한다.
>

```sql
SELECT * FROM A, B WHERE A.NO_EMP = B.NO_EMP;
```

### 3.1 교차 조인(CROSS JOIN)

![Untitled](https://file.notion.so/f/s/0e57eac5-86c8-42e7-b057-958e02a28ab8/Untitled.png?id=45d2c50a-df88-49ff-8985-aad5a8627fb9&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680480782064&signature=QKCyZq799p2ls1J5UG7dKzOOXlnSk0J4iLmhewG4-1s&downloadName=Untitled.png)

- 조인되는 두 테이블에서 곱집합을 반환한다.
- 예를 들어 m행을 가진 테이블과 n행을 가진 테이블 교차 조인되면 m*n개의 행을 생성한다.

명시적 조인 표현

```sql
SELECT * FROM MEMBER CROSS JOIN DISCORD;
```

암시적 조인 표현

```sql
SELECT * FROM MEMBER, DISCORD;
```

### 3.2 동등조인(EQUAL JOIN)

- 비교자 기반의 조인이며, 조인 구문에서 동등비교만을 사용합니다.
- 다른 비교 연산자( <와 같은)를 사용하는 것은 동등 조인으로서 조인의 자격을 박탈하는 것입니다.
- 위에 [내부 조인의 예시](https://www.notion.so/Join-27f1dcd8eec74c4d9e38abb7a4f0a41f)가 동등 조인입니다.

### 3.3 자연조인(NATURAL JOIN)

- 자연 조인은 동등 조인의 한 유형으로 두 테이블의 컬럼명이 같은 기준으로 조인 조건문이 암시적으로 일어나는 내부 조인입니다..
- 결과적으로 나온 조인된 테이블은 같은 이름을 가진 컬럼은 한 번만 추출된다.

### 3.4 비등가 조인 (NON-EQUI JOIN)

비등가 조인은 동등비교(=)를 사용하지 않는 조인으로 조건문이 크거나 작거나 같이 않은 비교등을 사용하면 비등가 조인이라고 합니다.

암시적 조인 표현

```sql
SELECT * FROM MEMBER, DISCORD;
WHERE MEMBER.TYPEID between 1 and 2;
```

## 4 외부 조인 (OUTER JOIN)

내부 조인의 경우에는 공통 컬럼명 기반으로 결과 집합을 생성합니다. 반면에 외부 조인은 조건문에 만족하지 않는 행도 표시해주는 조인입니다. 그래서, 조인을 했을 때 한쪽의 테이블에 데이터가 없어도 조인 결과에 포함시키는 조인입니다. 외부 조인은  3가지 종류가 있고 각각에 대해서 예제를 통해서 알아보도록 하겠습니다.

### 4.1 왼쪽 외부 조인 (LEFT OUTER JOIN)
![LEFT OUTER JOIN](https://file.notion.so/f/s/3b1d75ba-9fb3-406d-a477-94b4037f3a1e/Untitled.png?id=0126930f-e5b6-4bd9-8d47-335cbb6c3b48&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680490407468&signature=aQhP92bS4ctJXskr5QZlkt0IAcwWAenXlj1zaf8lCiA&downloadName=Untitled.png)
왼쪽 외부 조인은 테이블 A의 모든 데이터와 테이블 B와 매칭이 되는 레코드를 포함하는 조인입니다.

```sql
SELECT
A.NAME, B.AGE
FROM EX_TABLE A
LEFT OUTER JOIN JOIN_TABLE B ON A.NO_EMP = B.NO_EMP
```

### 4.2 오른쪽 외부 조인 (RIGHT OUTER JOIN)
![RIGHT OUTER JOIN](https://file.notion.so/f/s/b59da423-6f7e-4224-9e59-db397d90094b/Untitled.png?id=175d9535-69ab-4c70-9765-9e26cfa9dacc&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680490455072&signature=8Lcc-51rnOYax1TdweohMoWr5lNNHZCbA2NtUNAFX5E&downloadName=Untitled.png)
왼쪽 외부 조인은 테이블 B의 모든 데이터와 테이블 A와 매칭이되는 레코드를 포함하는 조인입니다.

### 4.3 완전 외부 조인 (FULL OUTER JOIN)
![FULL OUTER JOIN](https://file.notion.so/f/s/359cbe09-25dc-4a67-853f-577cee3b64f5/Untitled.png?id=20b638b0-6f67-46d6-978d-e1f64a1c5aa4&table=block&spaceId=3088add6-d1f4-432c-8ae5-86a51f66d543&expirationTimestamp=1680490484121&signature=ZoiEh6CaCBxFha2o9dCZPIcq7LTVfa7vrkK1Q3whFfs&downloadName=Untitled.png)
완전 외부 조인은 MySQL에서는 명시적인 SQL 구문은 지원하지 않지만, UNION을 사용해서 완전 외부 조인을 할 수 있습니다.

```sql
# 방법1 : JOIN와 UINION
SELECT *
FROM table1
  LEFT OUTER JOIN table2
    ON table1.n = table2.n
UNION
SELECT *
FROM table1
  RIGHT OUTER JOIN table2
    ON table1.n = table2.n;

# 방법2 : UNION ALL and exclusion join
SELECT *
FROM table1
  LEFT OUTER JOIN table2
    ON table1.n = table2.n
UNION ALL
SELECT *
FROM table1
  RIGHT OUTER JOIN table2
    ON table1.n = table2.n
WHERE table1.n IS null;
```

### 4.4 셀프조인

셀프 조인은 자기 자신과 조인하는 조인입니다. 예를 들면, 임직원중에 같은 부서에서 일하는 직원을 알고 싶으면 셀프 조인을 사용하면 좋습니다.

```sql
-- 셀프 조인(SELF JOIN)
# 암묵적 표현법 (implicit notation)

SELECT A.first_name AS EmployeeName1, B.first_name AS EmployeeName2, A.dept_no
FROM employees AS A, employees AS B
WHERE A.emp_no <> B.emp_no
AND A.dept_no = B.dept_no;
```

### 4.5  안티조인(ANTI JOIN)

안티 조인은 서브 쿼리내에서 존재하지 않는 데이터만 추출하여 메인 쿼리에서 추출하는 조인입니다.

### 4.6 세미 조인 (SEMI JOIN)

세미 조인은 안티 조인과 반대로 서브 쿼리 내에서 존재하는 데이터만을 가지고 메인 쿼리에서 추출하는 방식입니다.