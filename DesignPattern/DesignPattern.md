1.디자인 패턴 ?
====
1.1. 디자인 패턴이란
-
프로그램을 설계할 때 발생했던 문제점들을 객체 간의 상호 관계 등을 이용하여 해결할 수 있도록 하나의 '규약' 형태로 만들어 놓은 것  

1.2. 디자인 패턴 종류
-
### 1.2.1 GoF 디자인 패턴
- 에리히 감마(Erich Gamma), 리차드 헬름(Richard Helm), 랄프 존슨(Ralph Johnson), 존 블리시디스(John Vissides) 소프트웨어 개발 영역에서 디자인 패턴을 구체화하고 체계화한 사람들
- 종류
  - 생성 - 객체 생성과 관련된 패턴
    - 추상 팩토리
    - 빌더
    - 팩토리 메서드 : [Factory](Factory.md)
    - 프로토타입
    - 싱글톤 : [Singleton](Singleton.md)
  - 구조 - 클래스나 객체를 조합해 더 큰 구조를 만드는 패턴
    - 어댑터
    - 브리지
    - 컴퍼지트
    - 데코레이터
    - 퍼사드
    - 플라이웨이트
    - 프록시 : [Proxy](ProxyPattern.md)
  - 행위 - 객체나 클래스 사이 알고리즘이나 책임 분배에 관련된 패턴
    - 옵저버 : [Observer](ObserverPattern.md)
    - 책임 연쇄
    - 커맨드
    - 인터프리터
    - 이터레이터 : [Iterator](IteratorPattern.md)
    - 미디에이터
    - 메멘토
    - 상태
    - 전략 : [Strategy](StrategyPattern.md)
    - 템플릿
    - 방문자
### 1.2.2 MVC 패턴
  - MVC 패턴 : [MVC 패턴](MVCPattern.md)

### 1.2.3 MVP 패턴
  - MVP 패턴 : [MVP 패턴](MVPPattern.md)

### 1.2.4 MVVM 패턴
  - MVVM 패턴 : [MVVM 패턴](MVVMPattern.md)