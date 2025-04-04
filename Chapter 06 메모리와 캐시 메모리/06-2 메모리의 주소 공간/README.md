# 06-2 메모리의 주소 공간

## 📌 학습 목표

- 해당 챕터의 개념 정리

## ❓ 확인 문제


### Q1. JJH씨는 메모리 3번대 대장으로 근무지 발령을 받았다.

### JJH씨에게는 메모리 3번의 논리 주소가 적힌 표가 있고 이를 통해 메모리 3번의 물리주소를 찾아가야 한다.

### 메모리 3번의 물리주소는 몇번인가?

| 세그먼트 번호 | 베이스 주소 (Base Address) | 논리주소 |
| ------------- | -------------------------- | -------- |
| 0             | 2000                       | 500      |
| 1             | 3000                       | 800      |
| 2             | 4000                       | 700      |
| 3             | 5000                       | 300      |
| 4             | 6000                       | 1000     |


<details>
<summary>정답</summary>


- **5300번 **

**[해설]**

- 물리 주소 = **5000 + 300 = 5300**

# 🧠 **논리 주소 (Logical Address)와 물리 주소 (Physical Address)**

컴퓨터 시스템에서 메모리 관리 방식을 이해하기 위해, **논리 주소**와 **물리 주소**는 매우 중요한 개념입니다.

---

## ✅ **논리 주소 (Logical Address)**

- **논리 주소**는 CPU에서 생성된 주소입니다. 프로그램에서 사용하는 주소라고도 할 수 있습니다.
- 운영체제가 메모리 관리 기법을 통해 **논리 주소**를 실제 물리적인 메모리 주소로 변환합니다.
- CPU는 **논리 주소**만을 알며, 이 주소는 **가상 메모리** 시스템에서 사용됩니다.
- 논리 주소는 **페이지 번호**와 **오프셋**(또는 **세그먼트 번호**와 **오프셋**)으로 구성됩니다.

### 예시:

- 논리 주소 (1, 500)
  - 페이지 번호 1, 오프셋 500

---

## ✅ **물리 주소 (Physical Address)**

- **물리 주소**는 실제 메모리 칩에 저장되는 주소입니다.
- 운영체제가 MMU (Memory Management Unit)나 **베이스 레지스터** 등을 이용하여 **논리 주소**를 **물리 주소**로 변환합니다.
- 실제 RAM에서 데이터가 저장되는 위치를 나타냅니다.

## ✅ **논리 주소 → 물리 주소 변환**


**논리 주소**는 물리 주소로 변환될 때, 주로 **페이지 테이블**이나 **세그먼트 테이블**이 사용됩니다.  
이를 통해 논리 주소가 물리 주소로 어떻게 변환되는지 설명하겠습니다.

### 예시 1: 페이지 방식 주소 변환

- 페이지 크기: 1024바이트
- 논리 주소: 1500
- 페이지 번호: `1500 ÷ 1024 = 1` (몫)
- 오프셋: `1500 % 1024 = 476` (나머지)
- 페이지 테이블에서 페이지 1번의 **프레임 번호**가 7번이라고 하면, 물리 주소는 `7 × 1024 + 476 = 7204`가 됩니다.

### 예시 2: 세그먼트 방식 주소 변환

- 세그먼트 크기: 1000바이트
- 논리 주소: (3, 600)
  - 세그먼트 번호: 3
  - 오프셋: 600
- 세그먼트 3의 **베이스 주소**가 5000이라면, 물리 주소는 `5000 + 600 = 5600`이 됩니다.

---


## 🔥 **결론**

- **논리 주소**는 프로그램에서 사용되는 주소이며, 물리 메모리 상에서 실제로 어떤 주소인지 알 수 없습니다.
- **물리 주소**는 실제 메모리 칩에서 데이터가 저장되는 위치를 의미합니다.
- 운영체제는 **페이지 테이블**이나 **세그먼트 테이블**을 통해 논리 주소를 물리 주소로 변환하며, 이를 통해 **가상 메모리**를 효율적으로 관리합니다.

---

</details>

### Q2. 메모리와 CPU가 사용하는 주소에는 물리 주소와 논리 주소가 있다. 메모리는 물리 주소를 사용하며, CPU는 논리 주소를 사용하여 CPU의 메모리 간 상호작용을 위해 주소 간 변환이 필요하다. 다음 중 논리 주소와 물리 주소 간 변환을 수행하는 CPU와 주소 버스 사이 위치한 하드웨어는 무엇인가?

#### 1. SSD

#### 2. SDRAM

#### 3. MMU

#### 4. HTTP

<details>
<summary>정답</summary>

#### 3. MMU

- MMU(Memory Management Unit)는 메모리 관리 장치로, 논리 주소와 물리 주소 간 변환을 수행하는 하드웨어입니다.
- MMU는 CPU가 발생시킨 논리 주소에 베이스 레지스터 값을 더하여 논리 주소를 물리 주소로 변환할 수 있습니다.
- 이때 베이스 레지스터는 메모리 상에서 해당 프로그램의 첫 물리 주소를 갖습니다.

---

</details>


### Q3. 다른 프로그램의 영역을 침범할 수 있는 명령어는 위험하다. 그래서, 논리 주소 범위를 벗어나는 명령어 실행을 방지하고, 실행 중인 다른 프로그램에 영향을 받지 않도록 보호할 방법으로 이용하는 것은 무엇인가?


<details>
<summary>정답</summary>

#### 한계 레지스터

**[해설]**


- CPU가 메모리에 접근하기 전, 논리 주소가 한계 레지스터보다 작은지를 검사한다.
  만약 벗어난다면 인터럽트를 발생시켜, 실행을 중단하게 된다.


</details>

### Q4. 메모리 주소 공간에 대한 설명으로 틀린 것은?

1️. 논리 주소(Logical Address)는 프로그램이 인식하는 주소이며, 실행 중에는 물리 주소로 변환된다.

2️. MMU(Memory Management Unit)는 논리 주소를 물리 주소로 변환하는 역할을 한다.

3️. 한계 레지스터(Limit Register)는 프로세스가 접근할 수 있는 최대 메모리 크기를 지정한다.

4. 베이스 레지스터(Base Register)는 프로세스의 논리 주소 범위를 제한하는 역할을 한다.

<details>
<summary>정답</summary>


**4. 베이스 레지스터(Base Register)는 프로세스의 논리 주소 범위를 제한하는 역할을 한다. X**

- 베이스 레지스터는 논리 주소를 물리 주소로 변환할 때, 기준이 되는 시작 주소를 저장하는 레지스터입니다.
- 프로세스의 주소 제한을 담당하는 것은 **한계 레지스터(Limit Register)**입니다.

**[해설]**

**1. 논리 주소(Logical Address)는 프로그램이 인식하는 주소이며, 실행 중에는 물리 주소로 변환된다.**

- 프로그램이 인식하는 주소이며, 실행 중에는 **물리 주소(Physical Address)**로 변환됨

**2️. MMU(Memory Management Unit)는 논리 주소를 물리 주소로 변환하는 역할을 한다.**

- CPU가 생성한 논리 주소를 실제 물리 주소로 변환하는 역할을 수행
- 페이징, 세그먼테이션 등의 메모리 관리 기법과 연계됨

**3. 한계 레지스터(Limit Register)는 프로세스가 접근할 수 있는 최대 메모리 크기를 지정한다.**

- 프로세스가 접근할 수 있는 **최대 메모리 크기(주소 범위)**를 제한하여 메모리 보호 기능을 수행
- 한계 레지스터보다 큰 주소에 접근하려 하면 운영체제가 오류(예: segmentation fault)를 발생시킴

---

</details>

### Q5. 한 프로세스의 베이스 레지스터 값이 10,000이고 한계 레지스터 값이 4,000일 때, 다음 논리주소의 물리주소를 구하고, 접근 가능 여부를 판단하시오.

**1. 논리주소: 2,500** <br>
**2. 논리주소: 3,800** <br>
**3. 논리주소: 4,500**

<details>
<summary>정답</summary>

**1. 물리주소: 12,500 / 접근 가능** <br>
**2. 물리주소: 13,800 / 접근 가능** <br>
**3. 물리주소: 14,500 / 접근 불가능**

**[해설]**


#### 물리주소 = 베이스 레지스터 값 + 논리주소

#### 단, (논리주소 &le; 한계 레지스터 값)인 경우에만 접근 가능

**1. 물리주소=10,000+2,500=12,500** <br>
**논리주소(2,500) &lt; 한계 레지스터 값(4,000) -> 접근 가능**

**2. 물리주소=10,000+3,800=13,800** <br>
**논리주소(3,800) &lt; 한계 레지스터 값(4,000) -> 접근 가능**

**3. 물리주소=10,000+4,500=14,500** <br>
**논리주소(4,500) &gt; 한계 레지스터 값(4,000) -> 접근 불가능**

---

</details>


### Q6. 프로그램의 물리 주소 범위가가 정확한 것은?

#### 1. 한계 레지스터 값 이상 / 베이스 레지스터 값 + 한계 레지스터 값 미만

#### 2. 베이스 레지스터 값 이상 / 베이스 레지스터 값+한계 레지스터 값 미만

#### 3. 베이스 레지스터 - 한계 레지스터 값 이상 / 한계 레지스터 값 미만

#### 4. 한계 레지스터 - 베이스 레지스터 값 이상 / 베이스 레지스터 값 미만

<details>
<summary>정답</summary>

#### 2. 베이스 레지스터 값 이상 / 베이스 레지스터 값+한계 레지스터 값 미만

- 베이스 레지스터가 실행 중인 프로그램의 가장 작은 물리 주소를 저장하면, 한계 레지스터는 논리 주소의 최대 크기를 저장함.

- CPU가 접근하려는 논리주소는 한계 레지스터가 저장한 값보다 커서는 안된다! (만약 한계 레지스터보다 높은 논리 주소에 접근하려고 하면 인터럽트(트랩)을 발생시켜 실행을 중단시킴킴)

---

</details>

### Q7. 한계 레지스터는 논리 주소 범위를 넘어가는지 검사를, 베이스 레지스터는 논리 주소를 물리 주소로 변환하는 역할을 한다. 이 두 레지스터는 MMU와는 관계없이 동작하는 장치이며 MMU는 단지 주소 버스와 실제 RAM을 연결하는 역할을 한다
\[O, X]

<details>
	<summary>정답</summary>
	<h4>X</h4>
	---
	
	- 한계 레지스터와 베이스 레지스터 모두 MMU를 구성하는 부품이다. 각각의 레지스터의 동작을 통해 논리 주소를 물리 주소로 변환하는 역할을 하는 장치가 MMU이다.
</details>


### Q8. 한계 레지스터 값(논리 주소 크기)은 어떻게 결정되는가?

<details> 
<summary>정답</summary>

1️⃣ 프로그램의 컴파일/링크 단계에서 크기가 결정됨
- **프로그램이 컴파일되고 링킹된 결과(실행 파일)**에는 코드, 데이터, 스택 등의 크기 정보가 포함되어 있음.
- 운영체제는 프로그램 실행 요청을 받을 때, **실행 파일의 메타데이터(헤더)**를 읽어서 해당 프로그램이 필요로 하는 **전체 메모리 크기(논리 주소 공간)**를 확인함.

2️⃣ 동적 메모리 할당은 포함되지 않음
- 초기 한계 레지스터 값은 프로그램이 처음 실행될 때의 크기로 설정됨.
- 하지만 프로그램 실행 도중, 예를 들어 **동적 메모리 할당(malloc 등)**으로 더 많은 메모리를 요청하면:
    * 이는 메모리 관리자가 페이지 테이블 등으로 관리하게 되며, 한계 레지스터 값 자체는 실행 중 바뀌지 않는 경우가 많음.
    * 현대 시스템에서는 가상 메모리를 사용해 한계 레지스터 대신 페이지 테이블 기반 보호 기법을 사용하기도 함.

</details> 

---
## 📝 사용법

### 이렇게 활용해 보세요! ✨

1. ❓ 확인 문제 아래에 본인이 만든 질문을 추가하세요.
2. 설명이 길어질 경우, 따로 마크다운 파일을 만들고 링크를 함께 추가해 주세요! 🔗

### 🔗 링크 추가 방법

1. 먼저 질문을 작성합니다.
2. 링크를 적용할 문장을 마우스로 선택합니다.
3. URL을 붙여넣습니다.
4. 마크다운 형식으로 `[내용](링크)` 형태로 정리됩니다.

