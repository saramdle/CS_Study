# 🎯 중앙처리장치(CPU) 작동 원리
- - -

CPU(Central Processing Unit)는 산술논리연산장치, 제어장치, 레지스터로 구성되어 있는 컴퓨터 장치를 말하며, 인터럽트에 의해 단순히 메모리에 존재하는 명령어를 해석해서 실행하는 일꾼이다.

<br>

### ⭐ 제어장치
제어장치(CU, Control Unit)는 프로세스 조작을 지시하는 CPU의 한 부품이다. 입출력장치 간 통신을 제어하고 명령어들을 읽고 해석하며 데이터 처리를 위한 순서를 결정한다.
<br>

### ⭐ 레지스터
레지스터는 CPU 안에 있는 매우 빠른 임시기억장치를 말한다. CPU와 직접 연결되어 있으므로 연산 속도가 메모리보다 수십 배에서 수백 배까지 빠르다. CPU는 자체적으로 데이터를 저장할 방법이 없기 때문에 레지스터를 거쳐 데이터를 전달한다.
<br>

### ⭐ 산술논리연산장치
산술논리연산장치(ALU, Arithmetic Logic Unit)는 덧셈, 뺄셈 같은 두 숫자의 산술 연산과 배타적 논리합, 논리곱 같은 논리 연산을 계산하는 디지털 회로입니다.
<br>
<br>

* CPU 연산 처리 <br>

<img width="35%" src="https://user-images.githubusercontent.com/55771326/227506030-98cf9b4f-23c9-43ff-806d-d936cda711f0.jpeg">

<br>

1️⃣ 제어장치가 메모리에 계산할 값을 로드합니다. 또한, 레지스터에도 로드합니다. <br>
2️⃣ 제어장치가 레지스터에 있는 값을 계산하라고 산술논리연산장치에 명령합니다. <br>
3️⃣ 제어장치가 계산된 값을 다시 '레지스터에서 메모리로' 계산한 값을 저장합니다. <br>

<br>

### ⭐ 특수 목적 레지스터의 종류 <br>

✅ MAR (메모리 주소 레지스터) : 읽기와 쓰기 연산을 수행할 주기억장치 주소를 저장 <br>
✅ PC (프로그램 카운터) : 다음에 실행될 명령어의 주소를 저장 <br>
✅ SP (스택 포인터) : 스택의 최상위 주소를 저장 <br>
✅ IX (인덱스 레지스터) : 인덱스 주소 지정 방식에서 인덱스를 저장 <br>
✅ IR (명령어 레지스터) : 명령어를 호출해서 해독하기 위해 현재 명령어를 임시로 저장 <br>
✅ MBR (메모리 버퍼 레지스터) : 주기억장치의 내용을 임시로 저장하는 역할 <br>
✅ AC (누산기) : 산술 논리 장치의 연산 결과를 임시로 저장 <br>
✅ PSR (프로그램 상태 레지스터) : CPU의 현재 상태 정보를 저장 <br>

<br>

### ⭐ CPU가 하는 일은 요약해보면 대부분 고작 아래 4기능이 전부다. <br>

* 간단화 한 CPU Instruction Cycle(명령 주기)

<img src="https://i.namu.wiki/i/lxtQ_Cq9H5wWlZ-WxdWCjJOpLEBwD0YDrKSjS8TdU-2FYZJOhqWT5egZ-YwYeo81cnLUC7bd58An2whOU8Q_okVWBnMxKESbqCyrDxsjxtdCJ7KiU_x4xPQOGDaZAsOm4Mac4tI8eQ-jGKACgvWOxg.webp">


✅ Fetch(인출) : 메모리상의 프로그램 카운터가 가리키는 명령어를 CPU로 인출하여 적재 <br>
✅ Decode(해석) : 명령어의 해석. 이 단계에서 명령어의 종류와 타겟 등을 판단한다 <br>
✅ Execute(실행) : 해석된 명령어에 따라 데이터에 대한 연산을 수행한다 <br>
✅ Writeback(쓰기) : 명령어대로 처리 완료된 데이터를 메모리에 기록한다 <br>


### Reference
- - -
[나무 위키 - CPU](https://namu.wiki/w/CPU)