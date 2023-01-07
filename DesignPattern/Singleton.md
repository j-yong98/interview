싱글톤
=
싱글톤이란?
-
- 하나의 클래스에 오직 하나의 인스턴스만 가지는 패턴이다. 하나의 클래스를 기반으로 여러 개의 개별적인 인스턴스를 만들 수 있지만, 그렇게 하지 않고 하나의 클래스를 기반으로 단 하나의 인스턴스를 만들어 쓴다.  
- 하나의 인스턴스를 만들어 놓고 사용하면 다른 모듈들이 공유하며 사용하기 때문에 인스턴스를 생성할 때 드는 비용이 줄어드는 장점이 있다.  
- 하지만 의존성이 높아진다는 단점이 있다.  


예제
-

~~~
class Singleton {
    private static class singleInstanceHolder {
        private static final Singleton INSTANCE = new Singleton();
    }
    public static Singleton getInstance() {
        return singleInstanceHolder.INSTANCE;
    }
}
~~~
~~~
public class Main {
    public static void main (String[] args) {
        Singleton a = Singleton.getInstance();
        Singleton b = Singleton.getInstance();
        System.out.println(a.hashCode());
        System.out.println(b.hashCode());
        if (a == b) System.out.println(true);
    }
}

/*
705927765
705927765
true
*/
~~~

- 단점
  - 보통 TDD(Test Driven Development)를 할 때 걸림돌이 된다.
    - TDD를 할 때 주로 단위 테스트를 하는데 단위 테스트는 서로가 독립적이어야 하며 테스트를 어떤 순서로든 실행할 수 있어야 하기 때문이다.
    - 하지만 싱글톤 패턴은 미리 생성된 하나의 인스턴스를 기반으로 구현하는 패턴이기 때문에 각 테스트 마다 독립적인 인스턴스 생성이 어렵다.

의존성 주입
-
- 의존성이란 종속성이라고도 하며 A가 B에 의존성이 있다는 것은 B의 변경사항에 대해 A도 변경 해야 한다는 의미이다. 
- 싱글톤 패턴은 사용하기 쉽고, 실용적이지만 모듈 간의 결합을 강하게 만들 수 있다. 이 때 의존성 주입을 통해 모듈간의 결합을 조금 더 느슨하게 만들어 해결할 수 있다.
- 메인 모듈이 직접 하위 모듈에 직접 의존성을 주기 보다는 의존성 주입자가 이 부분을 담당해 '간접적'으로 의존성을 주입하는 방식
- 장점
  - 이를 통해 메인 모듈은 하위 모듈에 대한 의존성을 낮출 수 있다.
  - 모듈을 쉽게 교체할 수 있게 되고 테스팅이나 마이그레이션하기도 수월하다.
  - 구현할 때 추상화 레이어를 넣고 이를 기반으로 구현체를 넣어 주기 때문에 애플리케이션 의존성 방향이 일관되고, 쉽게 추론할 수 있으며, 모듈 간의 관계들이 조금 더 명확해진다.
- 단점
  - 모듈들이 더욱더 분리 되어 클래스 수가 늘어나 복잡성이 쉽게 증가할 수 있으며 약간의 런타임 패널티가 생기기도 한다.
- 의존성 주입 원칙
  - 상위 모듈은 하위 모듈에서 어떠한 것도 가져오지 않아야 한다.
  - 둘 다 추상화에 의존해야 한다. 이 때 추상화는 세부 사항에 의존하면 안된다.
