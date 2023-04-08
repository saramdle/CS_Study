# ✏️ 정규화 (Normalization)

---

### 정규화란 무엇일까?

정규화의 기본 목표는 `테이블 간의 중복된 데이터를 허용하지 않는 것입니다.` 중복된 데이터를 허용하지 않음으로 **무결성**을 유지할 수 있고 **DB의 저장 용량도 줄일 수 있습니다.**

테이블을 분해하는 정규화 단계가 정의되어 있습니다. 테이블이 어떻게 분해되는지에 따라 정규화 단계가 달라지는데 이번 포스팅을 통해 알아보도록 하겠습니다.

<br>

### 1️⃣ 제1 정규화

> 제1 정규화는 테이블의 컬럼이 원자값(Atomic Value, 하나의 값)을 갖도록 테이블을 분해하는 것입니다.

<table>
  <tr>
    <td>
        <img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbNbQUm%2FbtqT18yag04%2FpTXJX3wB23ouk8az7EgWQ1%2Fimg.png" />
    </td>
    <td>
        <img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbMlNZj%2FbtqT17FWVot%2FjUKTAUyOdrH83pRraKw3K0%2Fimg.png" />
    </td>
  </tr>
</table>

고객 취미 테이블이 존재한다고 가정해보겠습니다. 왼쪽 테이블에서 추신수와 박세리는 여러개의 취미를 가지고 있기 때문에 제1 정규형을 만족시키지 못하고 있습니다. 이를 제1 정규화를 통해 분해를 하게 되면 오른쪽과 같은 테이블로 구성이 될 수 있습니다.

<br>

### 2️⃣ 제2 정규화

> 제2 정규화란 제1 정규화를 진행한 테이블에 대해 완전 함수 종속을 만족하도록 테이블을 분해하는 것입니다. 여기서 완전 함수 종속이라는 것은 기본키의 부분집합이 결정자가 되어선 안된다는 것입니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FylbaZ%2FbtqT8Jc4K3s%2F0VFTPoKKFkbxZghKWDwKo1%2Fimg.png" />

테이블에서 기본키는 (학생번호, 강좌이름)으로 복합키입니다. 그리고 (학생번호, 강좌이름)인 기본키(복합키)는 성적을 결정하고 있습니다. 그런데 여기서 강의실 컬럼은 기본키의 부분집합인 강좌이름에 의해 결정될 수 있습니다.<br><br>

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbluCnc%2FbtqT7VEOf04%2FMe8DfY7rtycgJPYlYQKEWK%2Fimg.png" />

즉, 기본키(복합키)인 (학생번호, 강좌이름)의 부분키인 강좌이름이 결정자(강의실 컬럼 결정자)이기 때문에 위의 테이블 경우 기존의 테이블에서 강의실을 분해하여 별도의 테이블로 관리해서 제2 정규형을 만족시킬 수 있습니다.

<br>

### 3️⃣ 제3 정규화

> 제3 정규화란 제2 정규화를 진행한 테이블에 대해 이행적 종속을 없애도록 테이블을 분해하는 것입니다. 여기서 이행적 종속이란 A->B, B->C가 성립할 때 A->C가 성립되는 것을 말합니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FxUsSs%2Fbtrj4sJJchb%2FjZhQDFOYYSNkqM75cG87w0%2Fimg.png" />

위의 테이블을 보면 ID를 알면 등급을 알 수 있습니다. 마찬가지로 등급을 알면 할인율을 알 수 있습니다. 이행 종속성이 성립되기 때문에 해당 테이블은 제3 정규형을 만족하지 않습니다. 제3 정규형을 만족시키려면 ID를 통해 등급을 참조하고 등급으로 할인율을 참조할 수 있도록 테이블을 분해야하 합니다. 결과는 아래의 사진과 같습니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FdYnxPO%2FbtrP8O3VPDg%2FDfyMkh8K5mnKFBp35BOJYk%2Fimg.png" />

<br>

### 4️⃣ BCNF(Boyce-Codd Normal Form) 정규화

> BCNF 정규화란 제3 정규화를 진행한 테이블에 대해 모든 결정자가 후보키가 되도록 테이블을 분해하는 것입니다. 모든 결정자가 후보키가 되어야 한다는 뜻은 후보키 집합에 없는 컬럼이 결정자가 되어서는 안된다는 것입니다.

설명을 시작하기 전에 후보키가 무엇인지 궁금하실 수 있습니다. 예시를 들어서 이해하기 쉽게 후보키에 대해서 간단하게 설명해보겠습니다. 학생 컬럼에는 `학번, 주민번호, 이름, 성별`이 있다고 가정해보면 기본키가 될 수 있는 컬럼은 `학번, 주민번호`입니다. **즉, 기본키가 될 수 있는 키들을 후보키라고 합니다.**

이제 BCNF 정규화에 대해 사진과 함께 설명해보겠습니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbBN6xu%2FbtqT6IlqRF4%2FMvBoxYMxtgS1JT7t1AymnK%2Fimg.png" />

특강수강 테이블에서 기본키는 `(학생번호, 특강이름)` 입니다. 그리고 기본키 (학생번호, 특강이름)은 교수를 결정하고 있습니다. 그리고 교수는 특강이름을 결정하고 있습니다.

**문제는 교수 컬럼은 특강이름을 결정하는 결정자이지만 후보키가 아니라는 점입니다.** 그렇기 때문에 BCNF 정규화를 만족시키기 위해서 해당 테이블을 분해해야 합니다.

<img width="100%" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F3cbHr%2Fbtq3mNylPan%2Fc6b2lBuH4OkdDNmrzGHWUk%2Fimg.png" />

<br><br>

이 외에도 4정규화 이상이 있습니다. 하지만 보통 정규화는 BCNF까지만 하는 경우가 많다고 합니다. 그 이상의 정규화를 하면 정규화의 단점이 나타날 수도 있기 때문이라고 합니다.

---

## Reference

- https://mangkyu.tistory.com/110
- https://code-lab1.tistory.com/48
