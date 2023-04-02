# ✏️ SQL Injection

---

SQL Injection이란 악의적인 사용자가 보안상의 취약점을 이용해서 임의의 SQL 문을 주입하고 실행하게 해서 데이터베이스가 비정상적인 동작을 하도록 조작하는 행위를 말한다. 실제로 Injection 공격은 [OWASP](https://ko.wikipedia.org/wiki/OWASP) Top 10중 첫 번째에 속해있고 공격이 매우 쉬운 편이며 공격에 성공할 수록 큰 피해를 입을 수 있는 공격이다.

(위에서 언급한 OWASP는 오픈소스 웹 애플리케이션 보안 프로젝트라고 한다. 자세한 내용은 링크를 통해 확인!)

> - SQL: DB에서 사용하는 프로그래밍 언어
> - Injection: 무언가를 주입/주사할 때 사용하는 단어
> - SQL Injection = SQL + Injection = 프로그래밍 언어를 주입한다.

<br>

### 🔎 실제 사례

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99D4993C5C8890FB1D" />

실제로 2017년 3월에 국내 숙박 예약 플랫폼 회사인 "여기어때"에서 대규모 개인정보 유출 사건이 있었는데 SQL Injection으로 인한 피해라고 합니다.
자세한 내용은 해당 [뉴스](https://www.bloter.net/news/articleView.html?idxno=24731)에 잘 정리되어 있으니 궁금하신 분들은 확인하시면 좋을 것 같습니다.

<br>

### 🎈 SQL Injection 공격 기법

SQL Injection 공격에는 여러가지 공격 기법이 있습니다.
이번 포스팅에서는 잘 알려져있고 인기있는 공격 기법인 상위 3개 Injection만 다뤄보도록 하겠습니다.

- **Error based SQL Injection**
- **Union based SQL Injection**
- **Blind SQL Injection (Boolean based & Time based)**
- Stored Procedure SQL Injection
- Mass SQL Injection

<br>

1️⃣ **Error based SQL Injection**

- 논리적인 에러를 이용한 SQL Injection
- 가장 많이 쓰이고 대중적인 공격 기법입니다.
- 말 그대로 에러를 이용한 공격기법으로 고의로 SQL문에 에러를 발생시키는 기법입니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F9958373C5C8890FA03" />

위의 사진을 가지고 간단하게 설명드려보겠습니다. 위의 사진에서 1번 쿼리는 백엔드쪽에서 회원가입 또는 로그인 로직을 구현할 때 주로 사용하게 되는 쿼리입니다. 하지만 여기서 악의적인 사용자가 `OR 1=1 --`이라는 SQL 구문을 주입했습니다. 이로 인해 WHERE에 있는 조건들이 모두 참으로 만들어지고 --를 넣음으로서 뒤의 구문을 모두 주석처리하게 됩니다.

해당 SQL문이 주입되고 나면 3번 쿼리처럼 `SELECT * FROM Users`가 되고, Users 테이블에 있는 모든 정보를 조회할 수 있게 됩니다. 이렇게 되면 가장 먼저 만들어진 계정(관리자 계정)으로 로그인에 성공할 수 있게 됩니다. 보통은 관리자 계정을 맨 처음 만들기 때문에 관리자 계정에 로그인 할 수 있게 되고 또 다른 2차 피해로 연결될 가능성이 커진다.

<br>

2️⃣ **Union SQL Injection**

> UNION: 두 개의 쿼리문에 대한 결과를 통합해서 하나의 테이블로 보여주게 하는 SQL 키워드

- 공격하는 쿼리와 다른 쿼리를 결합해서 정보를 알아낼 때 사용하는 기법이다.
- 공격에 성공하기 위해서는 쿼리 두개의 컬럼 수와 데이터 형이 같아야 한다는 조건이 있다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99BD4C3C5C8890FA0A" />

위의 쿼리문은 Board 라는 테이블에서 게시글을 검색하는 쿼리문입니다. 입력값을 title과 contents 컬럼의 데이터와 비교하고 비슷한 글자가 있는 게시글을 출력합니다. 여기서 입력값으로 UNION 키워드와 함께 컬럼 수를 맞춰서 SELECT 구문을 넣어주게 되면 두 쿼리문이 합쳐져서 하나의 테이블로 보여지게 됩니다.

결과 쿼리는 `SELECT * FROM Board WHERE title LIKE '%' UNION SELECT null, id, password FROM Users --`가 됩니다. **결국 Injection이 성공하게 되면 사용자의 개인정보와 함께 게시글의 정보가 화면에 보여지게 됩니다.**

하지만 백엔드 쪽에서 비밀번호를 평문으로 저장하지는 않을겁니다. 그래도 Injection이 가능하다는 점에서 보안노출의 위험성이 있다고 생각합니다. 백엔드 단에서 입력값에 대한 검증을 했으면 해당 공격은 방어를 할 수 있지 않았을까 생각합니다.

<br>

3️⃣ **Blind SQL Injection - Boolean based Injection**

- 사용되는 SQL문: LIMIT, SUBSTR, ASCII 등
- 단순히 참과 거짓의 정보만 알 수 있을 때 사용한다. 해당 정보만을 통해 정보를 취득한다.
- 로그인 폼에 SQL Injection이 가능하다고 가정했을 때, 서버가 응답하는 로그인 성공과 로그인 실패 메세지를 이용해서 DB의 테이블 정보 등을 추출할 수 있습니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99525F3C5C8890F90E" />

임의로 abc123이라는 계정이 생성되었다고 가정하겠습니다. 악의적인 사용자는 `abc123’ and ASCII(SUBSTR(SELECT name From information_schema.tables WHERE table_type=’base table’ limit 0,1)1,1)) > 100 -- ` 이라는 구문을 주입합니다.

해당 구문은 MySQL에서 테이블 명을 조회하는 구문입니다. LIMIT 키워드를 통해서 하나의 테이블만 조회하고 SUBSTR 함수로 첫 글자만 가져오고 마지막으로 ASCII를 통해 ASCII 값으로 변환해줍니다. 만약에 조회되는 테이블 명이 User라고 한다면 U가 ASCII값으로 조회가 될 것이고, 뒤의 100이라는 숫자 값과 비교를 하게 됩니다. 거짓이라면 로그인 실패가 될 것이고 참이 될 때까지 뒤의 100이라는 숫자를 변경해가면서 비교를 하면 됩니다. 공격자는 이 프로세스를 자동화 스크립트를 통해서 단기간 내에 테이블 명을 알아낼 수 있습니다.

<br>

4️⃣ **Blind SQL Injection - Time based Injection**

- 사용되는 SQL문: SLEEP, BENCHMARK 등
- 응답의 결과가 항상 동일해서 해당 결과만으로 원하는 값을 판별할 수 없는 경우가 있을 수 있는데 이런 경우는 시간을 지연시키는 쿼리를 Injection해서 응답 시간의 차이로 참과 거짓여부를 판별할 수 있습니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99CAFB395C88914513" />

위의 사진에서는 Time based SQL Injection을 사용해서 현재 사용하고 있는 데이터베이스의 길이를 알아내는 방법입니다. 임의로 abc123이라는 계정이 생성되었다고 가정하겠습니다. 악의적인 사용자가 `abc123' OR (LENGTH(DATABASE()) = 1 AND SLEEP(2)) --` 이라는 SQL 구문을 주입했습니다. 여기서 LENGTH는 문자열의 길이를 반환하고, DATABASE는 데이터베이스의 이름을 반환합니다. <br>

3번 쿼리에서 LENGTH 부분이 참이면 SLEEP이 동작하고 거짓이면 동작하지 않을 것입니다. 여기서 숫자 1 부분을 조작하면서 데이터베이스의 길이를 알아낼 수 있습니다. 만약에 SLEEP이라는 단어가 치환처리 되어있다면 또 다른 방법으로 [BENCHMARK](https://www.habonyphp.com/2019/02/benchmark.html) 함수를 사용할 수 있습니다.

<br>

### 🎈 SQL Injection 대응 방안

1️⃣ **입력 값에 대한 검증**

SQL Injection 에서 사용되는 기법과 키워드는 엄청나게 많습니다. 그렇기 때문에 사용자의 입력 값에 대한 검증이 꼭 필요합니다.

2️⃣ **Prepared Statement 구문 사용**

Prepared Statement 구문을 사용하게 되면 사용자의 입력값이 데이터베이스의 파라미터로 들어가기 전에 DBMS가 미리 컴파일해서 실행하지 않고 대기합니다. 그 후 사용자의 입력값을 문자열로 인식하게 해서 공격쿼리가 들어간다고 해도 사용자의 입력은 이미 의미없는 단순 문자열이기 때문에 전체 쿼리문도 공격자의 의도대로 동작하지 않습니다.
`예시: INSERT INTO 테이블명 VALUES (?, ?, ?)`

[Statement와 PreparedStatement의 차이점](https://iksflow.tistory.com/127)

3️⃣ **Error Message 노출 금지**

공격자가 SQL Injection을 수행하기 위해서는 데이터베이스의 정보(테이블명 및 컬럼명 등)가 필요합니다. 데이터베이스 에러 발생 시 따로 처리를 해주지 않았다면 에러가 발생한 쿼리문과 함께 에러에 관한 내용을 반환해준다. 여기서 테이블명 및 컬럼명 그리고 쿼리문이 노출될 수 있기 때문에 데이터베이스에 대한 오류발생 시 사용자에게 보여줄 수 있는 페이지를 제작 혹은 메시지박스를 띄우도록 해야한다.

4️⃣ **웹 방화벽 사용**

웹 방화벽은 소프트웨어 형, 하드웨어 형, 프록시 형 이렇게 3가지 종류로 나눌 수 있습니다. 소프트웨어 형은 서버 내에 직접 설치하는 방법이고 하드웨어 형은 네트워크 상에서 서버 앞단에 직접 하드웨어 장비로 구성하는 것입니다. 마지막으로 프록시 형은 DNS 서버 주소를 웹 방화벽으로 바꾸고 서버로 가는 트래픽이 웹 방화벽을 먼저 거치도록 하는 방법입니다.

<br>

### 🎈 공부해보면서 느낀점

지금까지 SQL Injection에는 어떤 공격유형이 있고 대처법은 어떤게 있는지 살펴보았습니다. <br>
최근에 진행하고 있는 사이드 프로젝트(앱)에서 백엔드를 맡고 있는데 클라이언트 쪽으로 반환해주는 Response Message에서 에러가 발생하면 에러의 name과 stack을 반환해주도록 개발을 하고 있었습니다.

이번에 SQL Injection을 공부해보면서 Error Message를 노출하지 않는 것이 대응할 수 있는 방안이라고 하여 문제가 될 수 있는 부분이구나 라고 인지를 하고 수정을 해야겠다 판단했습니다.

---

## Reference

- https://kk-7790.tistory.com/74#article-2-0-1--1--error-based-sql-injection
- https://choco4study.tistory.com/10
- https://charming-kyu.tistory.com/18
