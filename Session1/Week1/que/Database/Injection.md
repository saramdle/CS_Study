# 🎯 SQL Injection
- - -
SQL Injection은 악의적인 사용자가 웹 애플리케이션의 입력 폼 등을 통해 SQL 쿼리문을 조작하여 데이터베이스에 대한 비인가된 접근 및 조작을 시도하는 공격 기법입니다.

<br>

### **_SQL Injection example_**
- - -
웹 애플리케이션에서 사용자가 입력한 값을 기반으로 SQL 쿼리문을 생성할 때, 사용자의 입력값이 그대로 쿼리문에 포함되는 경우에 발생할 수 있습니다. 악의적인 사용자는 입력값에 SQL 쿼리문을 포함시켜 데이터베이스를 조작할 수 있습니다. <br>
예를 들어, 다음과 같은 로그인 쿼리문이 있다고 가정해보겠습니다. <br>

```sql
SELECT * FROM users WHERE username = '사용자 입력값1' AND password = '사용자 입력값2'
```

이 때, 사용자 입력값1에 `' OR '1'='1'`을 입력하면 쿼리문은 다음과 같이 변경됩니다. <br>

```sql
SELECT * FROM users WHERE username = '' OR '1'='1' AND password = '사용자 입력값2'
```

이 경우, `'1':'1'` 은 항상 참이므로 WHERE 절이 항상 참이 되어 데이터베이스의 모든 사용자 정보가 반환될 수 있습니다. 이를 통해 악의적인 사용자는 로그인 정보를 알 수 있습니다.<br>

<br>

### **_SQL Injection 방어_**
- - -

1. Prepared Statements 사용: Prepared Statements는 입력값에 대한 SQL 쿼리문을 미리 컴파일하여 캐시에 저장하는 방식입니다. 이를 통해 입력값을 그대로 쿼리문에 포함시키는 대신, 쿼리문과 입력값을 별도로 전달하여 쿼리문 조작을 방지할 수 있습니다. <br>

````java
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM users WHERE username = ? AND password = ?");
stmt.setString(1, 사용자 입력값1);
stmt.setString(2, 사용자 입력값2);
ResultSet rs = stmt.executeQuery();
````

2. 입력값 검증: 입력값을 검증하여 쿼리문에 악의적인 코드가 포함되지 않도록 하는 방법입니다. 예를 들어, 사용자 입력값에 대해 정규식 검증을 수행하여 특수문자 등을 필터링할 수 있습니다. <br>

```javascript
if(!Pattern.matches("[a-zA-Z0-9]+", 사용자 입력값1)){
    // 사용자 입력값1에 특수문자가 포함되어 있을 경우 처리
}
```

이 외에도, 사용자 입력값을 인코딩하거나 SQL 쿼리문의 실행 권한을 최소한으로 부여하는 등의 방법을 사용하여 SQL Injection을 방어할 수 있습니다.