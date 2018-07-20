# 스프링 입문을 위한 자바 객체 지향의 원리와 이해
- [스프링 입문을 위한 자바 객체 지향의 원리와 이해](https://book.naver.com/bookdb/book_detail.nhn?bid=8920762)를 읽고 정리.
- 앞뒤 구분 없이 책을 읽으며 기억하고 싶은 내용을 쭉 적어 보았다.

## 신기술은 이전 기술의 어깨를 딛고
- 스프링을 비롯한 모든 신기술은 갑자기 하늘에서 뚝 떨어진 것이 아니다. 이전 기술의 어깨를 디딤돌 삼아 그 위에 이전 기술이 제시한 철학과 기법을 정반합의 논리로 정제하고, 이전 기술을 거름 삼아 새로운 철학과 기법을 더해 나타나는 것이다.
- 기계어 -> 어셈블리어 -> C언어(One Source Multi Object Use Anywhere) -> C++ 언어(객체지향 개념의 도입) -> 자바(진정한 객체 지향 언어, Write Once Run Anywhere)
- 위에 나열한 기술들 모두 없던 기술을 새롭게 만든 것이 아니다. 이전 기술의 어깨를 딛고 조금 더 사람들이 편하도록 발전하고 있음을 보여준다.

## 자바와 절차적/구조적 프로그래밍
- JDK : Java Development Kit / 자바 개발 도구 / JVM용 소프트웨어 개발 도구 / javac.exe 포함
- JRE : Java Runtime Environment / 자바 실행 환경 / JVM용 OS / java.exe 포함
- JVM : Java Virtual Machine / 자바 가상 기계 / 가상의 컴퓨터
- 자바 개발 도구인 JDK를 이용해 개발된 프로그램은 JRE에 의해 가상의 컴퓨터인 JVM 상에서 구동된다.
- 프로그램이 메모리를 사용하는 방식
    - 크게 코드 실행 영역과 데이터 저장 영역으로 나뉜다.
    - 객체 지향 프로그램에서는 데이터 저장 영역을 다시 세 개의 영역으로 분할해서 사용한다.
    - 스태틱(static) 영역, 스택(stack) 영역, 힙(heap) 영역

![javamemory](/images/javamemory.png)[그림 출처](http://asfirstalways.tistory.com/329)

- 구조적 프로그래밍은 함수를 써라는 것.
    - 함수를 쓰면 좋은 이유는 중복 코드를 한 곳에 모아서 관리할 수 있고, 논리를 함수 단위로 분리해서 이해하기 쉬운 코드를 작성할 수 있기 때문.
- 그럼 자바 언어에서 이러한 절차적 / 구조적 프로그래밍 유산은 어디에 남아 있을까? `메서드 내부`
- JRE는 먼저 프로그램 안에 main() 메서드가 있는지 확인. main() 메서드의 존재가 확인되면 JRE는 프로그램 실행을 위한 사전 준비에 착수한다.
    - 가상의 기계인 JVM에 전원을 넣어 부팅하는 것이다. 부팅된 JVM은 목적 파일을 받아 그 목적 파일을 실행한다. 
    - JVM이 맨 먼저 하는 일은 `전처리`라고 하는 과정이다. 
        - 모든 자바 프로그램이 반드시 포함하게 되는 패키지가 있다. `java.lang`패키지다.
        - JVM은 가장 먼저 java.lang 패키지를 메모리의 스태틱 영역에 가져다 놓는다.
        - 그 다음 import된 패키지를 메모리의 스태틱 영역에 배치
        - 프로그램 상의 모든 클래스를 메모리의 스태틱 영역에 배치
        - main() 메서드 스택 프레임 배치
        - 변수 공간 배치 등...
- main() 메서드 스택 프레임을 소멸시키는 블록 마침 기호인 닫는 중괄호가 보이면 메모리 소멸, JVM 기동 중지, JRE가 사용했던 시스템 자원을 운영체제에 반납하게 된다.
- 지역변수 : 스택 영역 (스택 프레임이 사라지면 함께 사라짐)
- 클래스 멤버 변수 : 스태틱 영역 (JVM이 종료될 때까지 고정)
- 객체 멤버 변수 : 힙 영역 (가비지 컬렉터가 회수할 때 까지)
- `외부 스택 프레임에서 내부 스택 프레임의 변수에 접근하는 것은 불가능하나 그 역은 가능하다.`
- __멀티 스레드의 메모리 모델은 스택 영역을 스레드 개수만큼 분해서 쓰는 것__
- 객체 지향 프로그래밍은 연산자, 제어문, 메모리 관리 체계 등 구조적 프로그래밍의 많은 부분을 차용하고 있다. 그리고 구조적 프로그래밍은 함수로 그 특징을 대변한다고 볼 수 있는데, 객체 지향 프로그래머들도 메서드 작성에 대한 지혜를 구조적 프로그래밍에서 배워와야 한다. 그러한 뜻에서 객체지향은 절차적 / 구조적 프로그래밍의 어깨를 딛고 만들어 졌다고 할 수 있다.
```
- 스태틱 : 클래스의 놀이터
- 스택 : 메서드의 놀이터
- 힙 : 객체의 놀이터
```

## 자바와 객체 지향
- 함수 : 코드를 논리적인 단위로 구분하고 분할해서 정복하자 - Divide and Conquer(분할 정복)
- 객체지향을 이해하기 위한 큰 그림
    - 세상에 존재하는 모든 것은 사물, 즉 객체(Object)다.
    - 각각의 사물은 고유하다.
    - 사물은 속성을 갖는다.
    - 사물은 행위를 한다.

### 객체 지향의 4대 특성 - 캡! 상추다
- 캡 : 캡슐화(Encapsulation) : 정보 은닉(information hiding)
- 상 : ~~상속(inheritance)~~ : 재사용
- 추 : 추상화(Abstraction) : 모델링
- 다 : 다형성(Polymorphism) : 사용 편의
- 클래스 vs 객체 = 붕어빵틀 vs 붕어빵 ??
    - 금형기계 붕어빵틀 = new 금형기계();
    - 새로운 금형기계를 하나 만들었더니 붕어빵틀이 되었다? X!
- 클래스는 분류에 대한 개념이지 실체가 아니다. 객체는 실체다.
    - 클래스 : 객체 = 펭귄 : 뽀로로 = 사람 : 김연아

### 추상화 : 모델링
- 추상 : 여러 가지 사물이나 개념에서 공통되는 특성이나 속성 따위를 추출하여 파악하는 작용
- 객체지향의 4대 특성은 클래스를 통해 구현됨.
- 객체 : 세상에 존재하는 유일무이한 사물
     - 이러한 객체는 생물이건 무생물이건 속성과 기능을 가지고 있다.
     - 객체 = 클래스의 인스턴스
- 클래스 : 분류, 집합. 같은 속성과 기능을 가진 객체를 총칭하는 개념
- `추상화란 구체적인 것을 분해해서 관심 영역에 대한 특성만을 가지고 재조합하는 것`
- 다시 IT 용어로 바꿔 보면
    - `추상화란 구체적인 것을 분해해서 관심 영역(애플리케이션 경계, Application Boundary)에 있는 특성만 가지고 재조합하는 것 = 모델링`
- 모델은 실제 사물을 정확히 복제하는 게 아니라 목적에 맞게 관심 있는 특성만을 추출해서 표현하는 것이다. 바로 모델은 추상화를 통해 실제 사물을 단순하게 묘사하는 것이다.
- 중요 사항
    - OOP의 추상화는 모델링이다.
    - 클래스 : 객체 = 펭귄 : 뽀로로
    - 클래스 설계에서 추상화가 사용된다.
    - 클래스 설계를 위해서는 애플리케이션 경계부터 정해야 한다.
    - 객체 지향에서 추상화의 결과는 클래스다.
- 추상화의 개념을 넓게 본다면
    - 상속을 통한 추상화, 구체화
    - 인터페이스를 통한 추상화
    - 다형성을 통한 추상화
- 자바는 객체 지향의 추상화를 어떻게 지원하고 있을까? `class` 키워드를 통해 지원하고 있다.
- `추상화 = 모델링 = 자바의 class 키워드`
- 결국 추상화를 통해 모델링을 하게 되면 아래 4가지 요소를 설계하게 되는 것이다.
    - 클래스 멤버 속성(staitc)
        - 예들들어, 쥐(동물) 클래스에서 쥐는 꼬리가 1개라는 속성은 변함없이 가짐.
        - 따라서 static int countOfTail = 1이라고 선언해서 쥐 클래스로 생성되는 여러 객체들에서 따로 선언없이 사용하도록 함.
    - 클래스 멤버 메서드(static)
    - 객체 멈버 속성
    - 객체 멤버 메서드
- static 키워드에 따라 클래스 멤버, 객체 멤버(변수, 메서드)로 구분
    - 클래스 멤버 = static 멤버 = 정적 멤버 : 객체가 아닌 클래스에 속해 있으며, 메모리의 스태틱 영역에 배치되기 때문에 객체의 존재 여부에 관계없이 쓸 수 있다.
    - 객체 멤버 = 인스턴스 멤버
- 스택 영역에 생기는 변수 = 지역변수 : 개발자가 별도로 초기화하지 않으면 쓰레기 값을 갖게 된다.
- 클래스 속성과 객체 속성은 별도의 초기화를 해주지 않아도 정수형은 0, 부동소수점형은 0.0, 논리형은 false, 객체는 null로 초기화된다. (공유 변수를 딱히 누가 초기화해야 한다고 규정할 수 없기 때문)

이름|다른이름|사는 곳(T 메모리)
---|---------|-------------
static 변수 | 클래스 [멤버] 속성, 정적 변수, 정적 속성... | 스태틱 영역
인스턴스 변수 | 객체 [멤버] 속성, 객체 변수... | 힙 영역
local 변수 | 지역 변수 | 스택 영역(스택 프레임 내부)

- 논리적 설계 : 개발 환경 (언어 등)에 영향을 받지 않는 설계
```
쥐
성명, 나이 , 꼬리수
울다()
```
- 물리적 설계 : 개발 환경에 맞춰진 설계
```
Mouse
+name : String, +age : int, +countOfTail : int
+ sing() : voide
```
### 상속: 재사용 + 확장
- 객체 지향에서의 상속은 상위 클래스의 특성을 하위 클래스에서 상속(특성 상속)하고 거기에 더해 필요한 특성을 추가, 즉 `확장`해서 사용할 수 있다는 의미
- 부모 - 자식 표현보다는 상위 - 하위, 슈퍼 - 서브라 표현하자.
- 상속 관계에서 반드시 만족해야 할 문장이 있다.
    - 하위 클래스는 상위 클래스다.
    - 아버지는 할아버지다??, 아들은 아버지다?? - 이상하다. (조직, 계층도)
        - 따라서 부모 - 자식 표현보다는 상위 - 하위, 슈퍼 - 서브라 표현하자는 것.
    - 포유류는 동물이다. 고래는 포유류다 - 자연스럽다.(분류도)
    - 객체 지향 설계 5원칙 가운데 LSP(리스코프 치환 원칙)을 나타내는 말.
- 자바 언어에서는 inheritance라는 키워드는 존재하지 않음. 대신 extends(확장)이 존재.
- is a 관계 보단 `is a kind of` 관계가 명확하다.
- 하위 클래스 is a kind of 상위 클래스
    - 해석: 하위 클래스는 상위 클래스의 한 분류다.
    - 펭귄 is a kind of 조류 -> 펭귄은 조류의 한 분류다.
    - 고래 is a kind of 동물 -> 고래는 동물의 한 분류다.
- 기억할 것
    - 객체 지향의 상속은 상위 클래스의 특성을 재사용하는 것이다.
    - 객체 지향의 상속은 상위 클래스의 특성을 확장하는 것이다.
    - 객체 지향의 상속은 is a kind of 관계를 만족해야 한다.
- 자바는 다중 상속을 지원하지 않는다.
    - 다중 상속의 [다이아몬드 문제](https://namu.wiki/w/%EC%83%81%EC%86%8D(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)) 때문.
    - 대신, 인터페이스를 도입해 다중 상속의 득은 취하고 실은 과감히 버림.

#### 상속과 인터페이스
- 인터페이스 : 구현 클래스 is able to 인터페이스
    - 해석 : 구현 클래스는 인퍼페이스를 할 수 있다.
    - 예 : 고래는 헤엄칠 수 있다.
- 언터페이스는 be able to, 즉 "무엇을 할 수 있는" 이라는 표현형태로 만드는 것이 좋다.
    - Serializable 인터페이스 : 직렬화할 수 있는
    - Comparable 인터페이스 : 비교할 수 있는
- 상위 클래스는 하위 클래스에게 특성 (속성과 메서드)을 상속해 주고, 인터페이스는 클래스가 '무엇을 할 수 있다'라고 하는 기능을 구현하도록 강제하게 된다.
- 상위 클래스는 물려줄 특성이 풍성할수록 좋고(LSP : 리스코프 치환 원칙), 인터페이스는 구현을 강제할 메서드의 개수가 적을수록 좋다(ISP : 인터페이스 분할 원칙)
- 논리적으로 이해하기 쉬운 코드 예
    - Penguin pororo = new Penguin();
        - 펭귄 한 마리가 태어나니 펭귄 역할을 하는 pororo라 이름 지었다.
    - pororo.name = "뽀로로";
        - pororo의 name을 "뽀로로"라 하자.
    - pororo.habitat = "남극";
        - pororo의 서식지를 "남극"이라 하자.
    - proro.showName();
        - pororo야 너의 이름을 보여다오.
    - pororo.showHabit();
        - pororo야 너의 서식지를 보여다오.

#### 상속과 메모리
- 메모리의 힙 상에 하위 클래스의 인스턴스가 생성될 때 상위클래스의 인스턴스도 같이 생성된다는 사실을 기억할 것. 

### 다형성 : 사용 편의성
- 객체 지향에서 다형성이라고 하면 오버라이딩(overriding)과 오버로딩(overloading)이라고 할 수 있다.
- 물론 상위 클래스와 하위 클래스 사이에서도 다형성을 이야기할 수 있고, 인터페이스와 그것의 구현 클래스 사이에서도 다형성을 이야기할 수 있지만 가장 기본은 오버라이딩과 오버로딩이다.
- 오버라이딩 : 같은 메서드 이름, 같은 인자 목록으로 상위 클래스의 메서드를 재정의
- 오버로딩 : 같은 메서드 이름, 다른 인자 목록으로 다수의 메서드를 중복 정의
- 상위 클래스 타입의 객체 참조 변수를 사용하더라도 하위 클래스에서 오버라이딩(재정의)한 메서드가 호출된다는 사실을 꼭 기억.
- 오버라이딩을 통한 메서드 재정의, 오버로딩을 통한 메서드 중복 정의를 통해 다형성을 제공하고 이 다형성이 개발자가 프로그램을 작성할 때 사용 편의성을 준다는 것.

### 캡슐화 : 정보 은닉
- 자바의 정보 은닉 (접근 제어자)
    - public : 모두가 접근 가능
    - protected : 상속 / 같은 패키지 내의 클래스에서 접근 가능
    - default : 같은 패키지 내의 클래스에서 접근 가능
    - private : 본인만 접근 가능
- 상속을 받지 않았다면 객체 멈버는 객체를 생성한 후 객체 참조 변수를 이용해 접근해야 한다.
- 정적 멤버는 클래스명.정적멤버 형식으로 접근하는 것을 권장한다.(일관된 형식으로 접근하기 위함)
    - 객체참조변수명.정적멤버 형태로도 접근할 수 있지만 권장되지 않음
    - 홍길동.인구수 보단 사람.인구로 접근하는 것이 권장됨.
- 참조 변수의 복사, `기억할 것`
    - 기본 자료형 변수는 값을 값 자체로 판단한다.
    - 참조 자료형 변수는 값을 주소, 즉 포인터로 판단한다.
    - 기본 자료형 변수를 복사할 때, 참조 자료형 변수를 복사할 때 일어나는 일은 같다. 즉, 가지고 있는 값을 그대로 복사해서 넘겨준다.
    - Call By Value와 Call By Reference를 다르다고 이해하기보다는 기본 자료형 변수는 저장하고 있는 값을 그 값 자체로 판단하고, 참조 변수는 저장하고 있는 값을 주소로 판단한다고 이해하기
