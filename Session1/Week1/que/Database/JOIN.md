# 🎯 JOIN

---

조인(Join)은 관계형 데이터베이스에서 두 개 이상의 테이블에서 데이터를 결합하여 하나의 결과 테이블을 생성하는 방법

**⭐️ 학생(student) 테이블**

| **id** | **name** | **major** |
| ------ | -------- | --------- |
| 1      | Alice    | English   |
| 2      | Bob      | Math      |
| 3      | Claire   | Science   |
| 4      | David    | History   |

**⭐️ 수업(course) 테이블**

| **id** | **course_name** | **instructor** |
| ------ | --------------- | -------------- |
| 1      | English 101     | Smith          |
| 2      | Math 101        | Johnson        |
| 3      | Science 101     | Lee            |
| 4      | History 101     | Kim            |

### ***INNER JOIN***

---

INNER JOIN은 두 테이블에서 일치하는 값만을 가져와서 결과 테이블을 생성합니다.

```sql
SELECT student.name, course.course_name
FROM student
INNER JOIN course ON student.major = course.course_name;
```

결과:

| **name** | **course_name** |
| -------- | --------------- |
| Alice    | English 101     |
| Bob      | Math 101        |
| Claire   | Science 101     |
| David    | History 101     |

### LEFT OUTER JOIN

---

LEFT OUTER JOIN은 왼쪽 테이블을 기준으로, 오른쪽 테이블과 일치하는 값만 가져오며, 오른쪽 테이블에 해당하는 값이 없을 경우에는 NULL 값을 반환합니다.

```sql
SELECT student.name, course.course_name
FROM student
LEFT OUTER JOIN course ON student.major = course.course_name;
```

결과:

| **name** | **course_name** |
| -------- | --------------- |
| Alice    | English 101     |
| Bob      | Math 101        |
| Claire   | Science 101     |
| David    | History 101     |
| Emma     | NULL            |

### RIGHT OUTER JOIN

---

RIGHT OUTER JOIN은 오른쪽 테이블을 기준으로, 왼쪽 테이블과 일치하는 값만 가져오며, 왼쪽 테이블에 해당하는 값이 없을 경우에는 NULL 값을 반환합니다.

```sql
SELECT student.name, course.course_name
FROM student
RIGHT OUTER JOIN course ON student.major = course.course_name;
```

결과:

| **name** | **course_name** |
| -------- | --------------- |
| Alice    | English 101     |
| Bob      | Math 101        |
| Claire   | Science 101     |
| David    | History 101     |
| NULL     | Art 101         |

### FULL OUTER JOIN

---

FULL OUTER JOIN은 왼쪽 테이블과 오른쪽 테이블에서 모든 값을 가져오며, 양쪽 테이블에서 일치하는 값이 없을 경우에는 NULL 값을 반환합니다.

```sql
SELECT student.name, course.course_name
FROM student
FULL OUTER JOIN course ON student.major = course.course_name;
```

결과:

| **name** | **course_name** |
| -------- | --------------- |
| Alice    | English 101     |
| Bob      | Math 101        |
| Claire   | Science 101     |
| David    | History 101     |
| Emma     | NULL            |
| NULL     | Art 101         |

### CROSS JOIN

---

CROSS JOIN은 두 테이블 간의 모든 조합을 반환합니다. 예를 들어, 학생 테이블과 수업 테이블에서 모든 학생과 모든 수업을 조합하여 결과를 반환하는 쿼리

```sql
SELECT student.name, course.course_name
FROM student
CROSS JOIN course;
```

결과:

| **name** | **course_name** |
| -------- | --------------- |
| Alice    | English 101     |
| Bob      | English 101     |
| Claire   | English 101     |
| David    | English 101     |
| Alice    | Math 101        |
| Bob      | Math 101        |
| Claire   | Math 101        |
| David    | Math 101        |
| Alice    | Science 101     |
| Bob      | Science 101     |
| Claire   | Science 101     |
| David    | Science 101     |
| Alice    | History 101     |
| Bob      | History 101     |
| Claire   | History 101     |
| David    | History 101     |
| Alice    | Art 101         |
| Bob      | Art 101         |
| Claire   | Art 101         |
| David    | Art 101         |

### SELF JOIN

---

SELF JOIN은 동일한 테이블을 두 번 조인하는 것입니다. 예를 들어, 학생 테이블에서 같은 전공을 가진 학생을 찾는 쿼리는 다음과 같습니다.

```sql
SELECT s1.name, s2.name
FROM student s1
JOIN student s2 ON s1.major = s2.major AND s1.id <> s2.id;
```

결과:

| **name** | **name** |
| -------- | -------- |
| Alice    | Bob      |
| Bob      | Alice    |
| Claire   | David    |
| David    | Claire   |

