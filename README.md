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
        // ...
    } else if (조건2) {
        // ...
    } else {
        // ...
    }
    ```
- Early return을 사용한다면 한 번에 하나의 조건만 신경쓰면되므로 뇌 메모리를 적게 쓸 수 있다.
  - ```java
    if (조건1) {
        // ...
        return;
    }
    if (조건2) {
        // ...
        return;
    }
    
    return;
    ```