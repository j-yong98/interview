프록시 패턴
=
프록시패턴이란?
-
- 대상 객체에 접근하기 전 그 접근에 대한 흐름을 가로채 대상 객체 앞단의 인터페이스 역할을 하는 디자인 패턴입니다.
- 이를 통해 객체의 속성, 변환 등을 보완하며 보안, 데이터 검증, 캐싱, 로깅에 사용합니다.
- 프록시 객체로도 사용 되지만 프록시 서버로도 활용됩니다.  

###### 프록시 서버의 캐싱 - 캐시 안에 정보를 담아두고, 캐시 안에 있는 정보를 요구하는 요청에 대해 더 멀리 있는 원격 서버에 요청하지 않고 캐시 안에 데이터를 활용하는 것을 말한다.

프록시 서버
-
- 프록시 서버는 서버와 클라이언트 사이에서 클라이언트가 자신을 통해 다른 네트워크 서비스에 간접적으로 접속할 수 있게 해주는 컴퓨터 시스템이나 응용프로그램을 가리킵니다.

예제
-
~~~
public interface Subject{
    void request();
}

public class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("Hello!");
    }
}

public class Proxy implements Subject {
    private Subject subject;
    
    @Override
    public void request() {
        if (this.subject == null) {
            return new RealSubject();
        }
        
        subject.request();
    }
}
~~~

~~~
public class Main {
    public static void main (String[] args) {
        Subject subject = new Proxy();
        subject.request();
    }
}
/*
Hello!
*/
~~~

### 프록시 서버를 설명하고 사용사례를 설명하시오.
***
프록시 서버란 서버 앞단에 둬서 캐싱, 로깅, 데이터 분석을 서버보다 먼저하는 서버를 말합니다.  
이를 통해 포트 번호를 바꿔서 사용자가 실제 서버의 포트에 접근하지 못하게 할 수 있으며 공격자의 DDOS 공격을 차단하거나 CDN을 프록시 서버로 달아서 캐싱처리를 용이하게 할 수 있습니다.
사용 사례는 nginx로 node.js를 이루어진 서버의 앞단에 둬서 버퍼 오버플로우를 해결하거나 CloudFlare를 둬서 캐싱, 로그 분석 등을 하는 사용사례가 있습니다.