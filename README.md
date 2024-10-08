# [인프런] Readable Code: 읽기 좋은 코드를 작성하는 사고법

<br><br>

## 학습정리
### 클린코드를 추구하는 이유
- 가독성
  - 글이 잘 읽힌다는 것은 이해가 잘 된다는 의미가 되기도 한다.
  - 이해가 잘된다면 보다 유지보수가 수월할 수 있다.
  - 이는 미래에 우리의 시간과 자원이 절약될 수 있다는 것을 의미하기도 한다.

### 추상
- 사물을 정확하게 이해하기 위해서 사물이 지니고 있는 여러 가지 측면 가운데서 특정한 측면만을 가려내어 포착하는 것이다.
- 다시말해 중요한 정보는 가려내어 남기고, 덜 중요한 정보는 생략하여 버린다는 의미가 될 수 있다.
- 읽기 좋은 코드(=클린코드)와 추상과의 관계
   - 적절한 추상화는 복잡한 데이터와 복잡한 로직을 단순화시켜 이해하기 쉬운 코드를 작성하는데 도움을 줄 수 있다.
- 잘못된 추상화
  - 추상화 과정에서 중요한 정보를 부각시키지 못하는 것
  - 해석자가 동일하게 공유하는 문맥이 없는 것(=공유되지 않은 도메인 지식, 자기만의 용어 사용 등)
  - 잘못된 추상화는 side-effect를 발생시킬 수 있다.

### 이름짓기
- 이름짓기는 가장 단순하면서도, 아주 중요한, 고도의 추상적 사고 행위이다.
- 이름짓기 팁
  - 단수와 복수 구분하기
    - 끝에 s를 붙여 어떤 데이터가 단수인지 복수인지를 나타낸다.
  - 이름 줄이지 않기
    - 줄임말은 때로는 가독성을 떨어트린다.
  - 은어 / 방언 사용하지 않기
    - 특정 사람들만 아는 용어는 사용하지 않는다.
    - 처음 접하게 되는 사람은 용어를 보고 의미를 유추하기 어려울 수 있다.
  - 좋은 코드를 보고 습득하기

### 메서드와 추상화
- 잘 쓰여진 글이라면, 한 문단의 주제는 반드시 하나다.
- 이와 비슷하게 잘 쓰여진 코드라면, 한 메서드의 주제도 반드시 하나다.
- 메서드에 주제가 여러개라면 의미를 담을 수 있는 작은 단위의 메서드로 잘게 쪼개야한다.
- 메서드명은 추상화된 구체를 유추할 수 있는 적절한 의미가 담긴 이름이 되야한다.
- 더 나아가 파라미터와 연결지어 더 풍부한 의미를 전달할 수도 있다.

### 추상화 레벨
- 하나의 세계(=메서드) 안에서는 추상화 레벨이 동등해야한다.
- Ex)
  - 아래 코드를 예시로 들자면 실제 구현되는 모드는 메서드로 분리가 되어있는 코드의 흐름이다가 갑자기 if문이 등장하며 구체화된 코드가 등장한다.
  - 이는 추상화 레벨이 동등하다고 볼 수 없다.
  ```java
  public static void main(String[] args) {
      showGameStartComments();
      initializeGame();
  
      // ...
  
      if (gameStatus == 1) { // 갑자기 구체화된 코드 등장
          // ...
      }
  }
  ```

### 매직 넘버, 매직 스트링
- 매직 넘버와 매직 스트링은 의미를 갖고 있으나 아직 상수로 추출되지 않은 숫자나 문자열을 뜻한다.
- 상수 추출로 이름을 짓고 의미를 부여함으로써 가독성과 유지보수성을 높일 수 있다.

### 뇌 메모리 적게 쓰기
- 뇌는 사실 한 번에 한 가지 일 밖에 하지 못한다.
- 뇌를 일종의 메모리라고 가정했을 때, 뇌에 적은 정보를 올릴 수 있게 코드를 작성할수록 좋은 코드가 된다고 볼 수 있다.
- 따라서 읽기 쉬운 코드는 좋은 논리구조와 가독성을 가져 뇌를 적게 쓸 수 있도록 하는 코드이다.
 
### Early return
- Early Return이란 조건과 맞지 않는 결과를 일찍 반환하는 것이다.
- 보통의 조건문은 앞서 존재하고 있는 조건을 기억하고 있어야한다. 이는 뇌 메모리를 적게 쓰자는 취지에서 벗어난다.
  - ```java
    if (조건1) {
        doSomething1();
    } else if (조건2) {
        doSomething2();
    } else {
        doSomething3();
    }
    ```
- Early return을 사용한다면 한 번에 하나의 조건만 신경쓰면되므로 뇌 메모리를 적게 쓸 수 있다.
  - ```java
    if (조건1) {
        doSomething1();
        return;
    }
    if (조건2) {
        doSomething2();
        return;
    }
    
    doSomething3();
    ```
    
### 사고의 depth 줄이기
- 중첩 분기문, 중첩 반복문
  - 중첩 분기문, 중첩 반복문이 있는 경우 사고의 depth를 줄이기 위해 메서드를 추출해서 표현할 수 있다.
  - 하지만 중첩문을 무조건 분리하라는 것은 아니다. 중첩문이 같이 위치해있을 때 의미가 더 명확하다면, 오히려 분리시키는 것이 혼선을 줄 수 있다.
    - ```java
      // 변경 전
      for (int i = 0; i < 10; i++) {
          for (int j = 0; j < 10; j++) {
              doSomething();
          }
      }
    
      // 변경 후
      for (int i = 0; i < 10; i++) {
          doSomethingWithI();
      }
      
      private void doSomethingWithI() {
          for (int j = 0; j < 10; j++) {
              doSomething();
          }
      }
      ``` 
- 변수
  - 사용할 변수는 사용 직전에 가깝게 선언하기
  - 변수 선언부와 사용부가 멀 경우 코드를 반복해서 왔다갔다하며 확인을 해야할 수 있다. (=코드를 작성하는데 효율이 떨어지게 된다.)

### 공백
- 공백 라인도 의미를 가진다.
- 복잡한 로직의 의미 단위를 나누어 보여줌으로써 읽는 사람에게 추가적인 정보를 전달할 수 있다.

### 부정어
- 부정어구를 쓰지 않아도 되는 상황인지 체크하기
- 부정 연산자 대신 부정의 의미를 담은 다른 언어가 존재하는지 고민하기(=부정어구로 메서드명 구성하기)
  - 부정 연산자를 대체할 수 있는 표현이 있다면, 대체 표현을 사용
  - Ex) if(!isLeft()) 대신 if(isRight())와 같이 부정 연산자 사용 지양

### 해피 케이스와 예외 처리
- 해피 케이스란 프로그램의 진행 방향이 우리가 원하는 베스트 케이스로 진행되는 상황을 뜻한다.
- 해피 케이스에만 집중하지 않고, 그 반대인 상황 예외 상황에 대한 처리를 꼼꼼히 하는 것이 견고한 프로그램을 만드는 것이다.
- 예외는 의도한 예외와 예상하지 못한 예외를 구분한다.
  - 사용자에게 보여줄 예외(=의도한 예외)와 개발자가 보고 처리해야할 예외(=예상하지 못한 예외)를 구분한다.
- Null
  - 항상 NullPointException을 방지하는 방향으로 경각심을 가져야한다.
  - 메서드 설계 시 return null을 자제한다.
  - 또는 Optional 사용을 고민해본다.
    - Optional은 비싼 객체이므로 꼭 필요한 상황에서만 반환 타입으로 사용해야한다.
    - Optional은 분기 케이스가 3개나 되기 때문에 파라미터로 받지 않도록 해야한다.
    - orElse(), orElseGet(), orElseThrow()의 차이를 숙지하고 사용한다.
      - orElse()는 항상 실행되므로 확정된 값일 때만 사용해야한다.
      - orElseGet()은 null인 경우만 실행된다.

### 추상의 관점으로 바라보는 객체 지향
- 객체란?
  - 추상의 관점에서 봤을 때, 추상화된 데이터와 코드의 조합이다.
- 협력과 책임
  - 객체는 객체 간의 협력과 객체가 담당하는 책임이 중요하다고 볼 수 있다.
- 객체지향의 특징
  - 객체 지향의 대표적 특징으로는 캡슐화, 추상화, 상속, 다형성이 있다.
  - 모두 추상화의 하위 개념으로도 볼 수 있다.
- 관심사의 분리
  - 관심사에 따라 기능과 책임을 토대로 객체를 만들 수 있다.
  - 관심사를 모았을 때, 관심사는 내부적으로 응집도가 높아야하며, 관심사끼리는 결합도가 낮아야한다.
  - 관심사가 적절히 분리되지 않았을 때는 기능변화가 있을 때, 변경으로 인한 영향이 크다는 것을 의미한다. (= 변경되는 코드가 많아져 유지보수 측면에서 좋지 못하다는 뜻)

### 객체 설계하기
- 객체로 추상화하기
  - 객체는 공개 메서드를 통해 외부 세상과 소통(=다른 객체와의 협력)한다.
  - 이는 공개 메서드에 객체에 책임이 녹아져있다고 볼 수 있다.
- 객체가 제공하는 것
  - 절차 지향에서 잘 보이지 않았던 개념을 가시화
  - 관심사가 한 군데로 모이기 때문에 유지보수성 향상
  - 여러 객체를 사용하는 입장에서는 구체적인 구현에 신경쓰지 않고 추상화 레벨에서 도메인 로직을 다를 수 있다.
- 객체를 만들 때 주의점
  - 1개의 관심사로 명확하게 책임이 정의되었는지 확인
  - 생성자와 정적 팩토리 메서드를 사용하면 메서드에서 유효성 검증이 가능하다.
  - Getter / Setter 사용 자제
    - 데이터는 불변이 최고이므로 가능한 Setter 사용을 지양하고, 외부에서 데이터 변경을 요청하는 경우 set~ 보다는 update~의 형태로 의도가 있는 네이밍을 활용한다.
    - Getter는 처음부터 추가하지 않고, 사용 시점에 추가한다.

### SOLID
- 객체 지향 설계를 더 유연한 형태로 만들 수 있는 원칙
  - SRP(Single Responsibility Principle)
    - 하나의 클래스는 단 한 가지의 변경 이유만을 가져야 한다.
    - 관심사 분리를 통해 하나의 객체는 하나의 책임만 가지도록 설계한다.
    - SRP를 지키게 되면 자연스레 높은 응집도와 낮은 결합도를 갖게된다. 
  - OCP(Open-Closed Principle)
    - 확장에는 열려 있고, 수정에는 닫혀 있어야 한다.
    - 기존 코드의 변경 없이, 시스템의 기능을 확장할 수 있어야 한다는 개념이다.
    - 추상화와 다형성을 활용해서 OCP를 지킬 수 있다.
  - LSP(Liskov Substitution Principle)
    - 상속 구조에서 부모 클래스의 인스턴스를 자식 클래스의 인스턴스로 치환할 수 있어야 한다.
    - LSP를 위반하면, 상속 클래스를 사용할 때 오동작, 예상 밖의 예외가 발생하거나, 이를 방지하기 위한 불필요한 타입 체크가 동반될 수 있다.
  - ISP(Interface Segregation Principle)
    - 클라이언트는 자신이 사용하지 않는 인터페이스에 의존하면 안 된다. (= 인터페이스를 잘게 쪼개라.)
    - ISP를 위반하면, 불필요한 의존성으로 인해 결합도가 높아지고 특정 기능의 변경이 여러 클래스에 영향을 미칠 수 있다.
  - DIP(Dependency Inversion Principle)
    - 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 된다.
    - 고수준, 저수준 모듈이 모두 추상화에 의존하는 것.
    - 저수준 모듈이 변경되어도 고수준 모듈에는 영향이 가지 않는다. (추상화가 되었다는 것은 저수준이라는 의미로 볼 수 있다.)

### 상속과 조합
- 상속보다 조합을 사용하자.
- 상속은 설계가 굳어지는 구조라서 수정이 어렵다. (부모와 자식의 결합도가 높다.)
- 조합과 인터페이스를 활용하는 것이 유연한 구조를 만들 수 있다.
  - 상속을 통한 코드의 중복 제거가 주는 이점보다 중복이 생기더라도 유연한 구조 설계가 주는 이점이 더 크다.

### Value Object
- 도메인의 어떤 개념을 추상화하여 표현한 값 객체
- Value Object는 훌륭한 추상화 기법 중 하나이다.
- 기본 타입을 객체로 한 번 감싸서 의미를 부여하는 추상화 기법이다.
- 동등성을 보장하기 위하여 equals() & hashCode()의 재정의가 필요하다.

### 일급 컬렉션
- 컬렉션을 포장하면서, 컬렉션만을 유일하게 필드로 가지는 객체
  - 컬렉션을 다른 객체와 동등한 레벨로 다루기 위함
  - 단 하나의 컬렉션 필드만을 가진다.
- 컬렉션을 추상화하며 의미를 담을 수 있고, 가공 로직의 보금자리가 생긴다.
- 만약 getter로 컬렉션을 반환할 일이 생긴다면, 외부 조작을 피하기 위해 새로운 컬렉션으로 만들어서 반환하는 것이 좋다.

### Enum의 특성과 활용
- Enum은 상수의 집합이며, 상수와 관련된 로직을 담을 수 있는 공간이다.
- 특정 도메인 개념에 대해 그 종류와 기능을 명시적으로 표현해줄 수 있다.
- 변경이 잦은면 Enum 보다 DB로 관리하는 것이 효율적일 수 있다.

### 숨겨져 있는 도메인 개념 도출하기
- 도메인 지식은 만드는 것이 아니라 발견하는 것.
- 객체 지향은 현실을 100% 반영하는 도구가 아니라, 흉내내는 것이다.
  - 현실 세계에서 쉽게 인지하지 못하는 개념도 도출해서 사용해야 할 때가 있다.
- 설계할 때는 근시적, 거시적 관점에서 최대한 미래를 예측하고, 시간이 지나 만약 틀렸다는 것을 인지하면 언제든 돌아올 수 있도록 코드를 만들어야 한다.

### 주석의 양면성
- 주석이 많다는 것은 그만큼 비즈니스 요구사항을 코드에 잘 못 녹였다는 이야기이다.
- 코드를 설명하는 주석을 쓰면 코드가 아니라 주석에 의존하게 된다. (코드를 명확하지 않게 작성하고 주석으로 부연설명을 하게된다.)
- 주석에 의존하여 코드를 작성하면 적절하지 않은 추상화 레벨을 갖게 되어 낮은 품질의 코드가 만들어진다.
- 주석을 작성할 때, 자주 변하는 정보는 최대한 지양해서 작성한다.
- 주석이 없는 코드보다, 부정확한 주석이 달린 코드가 더 치명적이다.
- 좋은 주석이란? 
  - 우리가 가진 모든 표현 방법을 총동원해 코드에 의도를 녹여내고, 그럼에도 불구하고 전달해야 할 정보가 남았을 때 사용하는 주석.

### 변수와 메서드의 나열 순서
- 변수는 사용하는 순서대로 나열한다.
- 메서드의 순서는 객체의 입장에서 고려해본다.
  - 객체는 협력을 위한 존재이다.
  - 외부 세계에 내가 어떤 기능을 제공할 수 있는지를 드러내기 때문에 공개 메서드를 상단에 배치하는 것을 고려해본다.
  - 공개 메서드끼리도 기준을 가지고 배치하는 것이 좋다.
    - 중요도 순, 종류별로 그룹화하여 배치하면 실수로 비슷한 로직의 메서드를 중복으로 만드는 것을 방지할 수 있다.
- 비공개 메서드는, 공개 메서드에서 언급된 순서대로 배치한다. 
  - 공통으로 사용하는 메서드라면, 규칙을 만들어 통일성 있게 배치한다.

### 패키지 나누기
- 패키지는 문맥으로써의 정보를 제공할 수 있다.
- 패키지를 쪼개지 않으면 관리가 어려워진다.
- 패키지를 너무 잘게 쪼개도 마찬가지로 관리가 어려워진다.
- 대규모 패키지 변경은 팀원과의 합의를 이룬 시점에 하자.
  - 여러 사람이 변경 중인 부분이나, 공통으로 사용하는 클래스들의 패키지를 한번에 변경하면, 추후 conflict가 생길 수 있다.
  - 처음 만들 때부터 잘 고민해서 패키지를 나눠놓는 것이 제일 좋다.

### IDE 도움받기
- 코드 스타일 자체도 가독성을 높일 수 있는 방법 중 하나이다.
- 코드 포맷 정렬 단축키를 사용하여, 코드 포맷을 맞춘다.
- 코드 품질 관련 플러그인인 Sonarlint를 사용하면, 잠재적으로 문제가 될 수 있는 오류, 버그 등을 미리 알려준다.
- editorconfig를 사용하여, 포맷 규칙을 정하고 여러 사람과 협업 시 사용하면 일관적인 코드 스타일을 유지할 수 있다.

### 능동적 읽기
- 복잡하거나 엉망인 코드를 읽고 이해하려 할 때, 리팩토링하면서 읽기
  - 눈으로만 코드를 읽는 것이 아니라 실제 리팩토링을 진행해보며 읽어본다. (롤백 기능이 있으니 코드를 뜯어가보며 읽자!)
    - 공백으로 단락 구분하기
    - 메서드와 객체로 추상화 해보기
    - 주석으로 이해한 내용 표기하며 읽기
- 핵심 목표는 우리의 도메인 지식을 늘리는 것과 동시에 이전 작성자의 의도를 파악하는 것.

### 오버 엔지니어링
- 오버 엔지니어링이란?
  - 필요한 적정 수준보다 더 높은 수준의 엔지니어링
    - Ex) 구현체가 하나인 인터페이스
      - 인터페이스 형태가 아키텍처 이해에 도움을 주거나, 근시일 내에 구현체가 추가될 가능성이 있는 것이 아니라면 오버 엔지니어링일 수 있다.
      - 코드 탐색에 영향을 주며, 애플리케이션이 비대해지는 결과를 초래할 수 있다.
    - Ex) 너무 이른 추상화
      - 정보가 숨겨지기 때문에 복잡도가 높아진다.
      - 후대 개발자들이 선대의 의도를 파악하기가 어렵다.

### 은탄환은 없다
- 클린코드도 은탄환이 아니다.
- 지속 가능한 소프트웨어의 품질 VS 기술 부채를 안고 가는 빠른 결과물
  - 대부분의 회사는 시장에서 빠르게 살아남는 것이 목표다.
  - 하지만 이런 경우에는 클린코드를 추구하지 말라는 것이 아니라, 미래 시점을 위해 적당한 적용을 시켜야한다는 것이다.
  - 결국은 클린 코드의 사고법을 기반으로 결정하는 것이 필요하다.