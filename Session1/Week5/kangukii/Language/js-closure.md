# JavaScript Closure (클로저)

---

클로저를 먼저 설명드리기 전에 Closure의 사전적 의미를 한번 찾아보았는데 `폐쇄`라는 뜻을 가지고 있었습니다. 자바스크립트에서도 마찬가지로 폐쇄와 유사한 의미를 가지고 있습니다.

### 1. Closure(클로저)란?

**한마디로 먼저 정리하자면 클로저는 `함수가 선언 또는 생성될 그 당시에 주변의 환경과 함께 갇히는 것`을 의미합니다.**

조금 더 자세하게 표현을 해보자면 `함수가 속한 Lexical Environment(렉시컬 스코프)를 기억해서 함수가 렉시컬 스코프 밖에서도 실행될 때도 이 스코프에 접근할 수 있게 해주는 기능`을 말합니다.

또 다른 클로저의 뜻으로는 `내부함수는 외부함수의 지역변수에 접근할 수 있는데 외부함수의 실행이 끝나서 외부함수가 소멸된 이후에도 내부함수가 외부함수의 변수에 접근할 수 있는 것`을 말합니다.

<br>

### 2. Lexical Environment (렉시컬 스코프)

> 함수를 어디서 호출하는지가 아니라 어디에 선언하였는지에 따라 결정되는 것을 말합니다.

> 다시 말해서, 함수를 어디서 선언하였는지에 따라 상위 스코프를 결정한다는 뜻이고 가장 중요한 점은 함수의 호출이 아니라 함수의 선언에 따라 결정된다는 점입니다.

```javascript
var x = 1; // 전역 변수

function first() {
  var x = 10;
  second();
}

function second() {
  console.log(x);
}

first();
second();
```

자바스크립트에서는 위의 코드에서 스코프를 결정합니다.

- global 범위에 있는 변수 x
- first 함수 안에 있는 변수 x
- second 함수 안에 있는 변수 x

위 예제의 실행 결과는 second 함수의 상위 스코프가 어디인지에 따라 결정됩니다.<br>
자바스크립트는 Lexical Scope를 따르기 때문에 함수를 선언한 시점에 상위 스코프가 결정됩니다.

`그렇기 때문에 second 함수가 first 함수 안에서 호출된 것과 상관없이 second 함수는 global 범위에 선언되어 있기 때문에 global 범위에 있는 X가 두 번 출력된 것입니다.`

<br>

### 3. 예시

```javascript
let numOne;
numOne = 1;

function addNumOne(num) {
  console.log(numOne + num);
}

addNumOne(5);
```

- 위 프로그램이 실행되면 Lexical 환경에 numOne 변수와 addNumOne 함수가 들어갑니다. 여기서 numOne은 초기화되지 않아서 사용이 불가능한 상태이고 addNumOne 함수는 사용가능한 상태가 됩니다.

```
<전역 Lexical 환경>
numOne: undefined
addNumOne: function
```

- 그리고 numOne에 1을 대입하면 Lexical 환경은 다음과 같이 됩니다.

```
<전역 Lexical 환경>
numOne: 1
addNumOne: function
```

- 그다음 마지막 라인의 addNumOne(5)가 실행되면 addNumOne이라는 새로운 Lexical 환경이 생성됩니다. `이 내부 환경은 함수가 넘겨받은 매개변수와 지역변수가 저장됩니다.`

```
<전역 Lexical 환경>
numOne: 1
addNumOne: function

<addNumOne Lexical 환경>
num: 5

<참조 방향>
addNumOne의 Lexical 환경 -> 전역 Lexical 환경
```

- addNumOne(5)의 Return 값으로 6이 나오는데 어떻게 나왔느냐? `addNumOne의 Lexical 환경에는 num 값이 있는데 numOne이 없으니까 numOne값을 전역 Lexical 환경에서 찾아온다.` 그래서 1+5로 6이 나오는 것입니다!

<br>

### 4. 활용되는 부분

> Closure는 대부분 실무 프론트 코드쪽에서? 사용되는 경우가 많다고 합니다. (구글피셜) 자신이 생성될 때의 환경을 기억해야 하기 때문에 메모리 적인 측면에서는 손해를 보지만 그래도 손해를 보는 만큼 강력한 기능을 가지고 있다고 합니다.

#### 상태유지

가장 유용하게 쓰이는 상황 중 하나는 현재 상태를 기억하고 있다가 상태가 변경되면 그것을 최신상태로 유지하는 것입니다.

```html
<!DOCTYPE html>
<html>
  <body>
    <button class="toggle">toggle button</button>
    <div class="txt">
      <h1>toggle test</h1>
    </div>

    <script>
      let txtField = document.querySelector(".txt");
      let toggleBtn = document.querySelector(".toggle");

      let toggle = (function () {
        let isVisable = false;

        // 1.클로저를 반환
        return function () {
          txtField.style.display = isVisable ? "block" : "none";
          // 3. 상태 변경
          isVisable = !isVisable;
        };
      })();

      // 2. 이벤트 프로퍼티에 클로저를 할당
      toggleBtn.onclick = toggle;
    </script>
  </body>
</html>
```

#### 데이터 은닉화

가끔 전역변수를 사용해서 변수를 공유할 때도 있을수도 있습니다. 전역변수를 사용하게 되면 오류가 발생활 확률이 엄청 높아지는데 그 이유가 누구든 전역변수에 접근할 수 있기 때문에 의도치 않게 값이 변경될 수 있기 때문입니다!

```html
<!DOCTYPE html>
<html>
  <body>
    <button id="plus">+</button>
    <p id="count">0</p>
    <script>
      let plusBtn = document.getElementById("plus");
      let countTxt = document.getElementById("count");

      let plus = (function () {
        // 카운트 상태를 유지하기 위한 자유 변수
        let count = 0;
        // 클로저를 반환
        return function () {
          return count++;
        };
      })();

      plusBtn.onclick = function () {
        countTxt.innerHTML = plus();
      };
    </script>
  </body>
</html>
```

위 예제는 숫자를 하나씩 카운트하는 코드입니다. 만약에 count 변수가 전역변수로 선언이 되어있었다면 위험한 코드였을 것인데 위의 코드처럼 `클로저를 사용해서 내부로 숨기면서 데이터를 은닉화 했습니다.`

객체지향 언어에서 private 키워드를 이용해 캡슐화시키는 것처럼 자바스크립트에서도 클로저를 이용하면 비슷한 기능을 구현할 수 있습니다.

---

### Reference

- https://devkingdom.tistory.com/331
- https://blacklobster.tistory.com/7
