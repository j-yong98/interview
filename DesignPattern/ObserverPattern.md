옵저버패턴(Observer Pattern)
=
옵저버 패턴이란?
-
- 주체가 어떤 객체의 상태 변화를 관찰하다가 상태 변화가 있을 때마다 메서드 등을 통해 옵저버 목록에 있는 옵저버들에게 변화를 알려주는 패턴
- 주체란 객체의 상태 변화를 보고 있는 관찰자이며, 옵저버들이란 이 객체의 상태 변화에 따라 전달되는 메서드 등을 기반으로 '추가 변화 사항'이 생기는 객체들을 의미한다.
- 주체와 객체를 따로 두지 않고 상태가 변경되는 객체를 기반으로 구축하기도 한다.
- 주로 이벤트 기반 시스템에 사용되며 MVC 패턴에도 사용됩니다.

예제
-
~~~
interface Subject {
    public void register(Observer obj);
    public void unregister(Observer obj);
    public void notifyObservers();
    public Object getUpdate(Observer obj);
}

interface Observer {
    public void update();
}

class Topic implements Subject {
    private List<Observer> observers;
    private String message;
    
    public Topic() {
        this.observers = new ArrayList<>();
        this.message = "";
    }
    
    @Override
    public void register(Observer obj) {
        if (!observers.contains(obj)) observers.add(obj);
    }
    
    @Override
    public void unregister(Observer obj) {
        observers.remove(obj);
    }
    
    @Override
    public void notifyObservers() {
        this.observers.forEach(Observer::update);
    }
    @Override
    public Object getUpdate(Observer obj) {
        return this.message;
    }
    
    public void postMessage(String msg) {
        System.out.println("Message sended to Topic : " + msg);
        this.message = msg;
        notifyObservers();
    }
}

class TopicSubscriber implements Observer {
    private String name;
    private Subject topic;
    
    public TopicSubscriber(String name, Subject topic) {
        this.name = name;
        this.topic = topic;
    }
    
    @Override
    public void update() {
        String msg = (String) topic.getUpdate(this);
        System.out.println(name + ":: got message >> " + msg);
    }
}
~~~

~~~
public class Main {
    public static void main (String[] args) {
        Topic topic = new Topic();
        Observer a = new TopicSubscriber("a", topic);
        Observer b = new TopicSubscriber("b", topic);
        Observer c = new TopicSubscriber("c", topic);
        
        topic.register(a);
        topic.register(b);
        topic.register(c);
        
        topic.postMessage("amumu is op champion!");
    }
}
/*
Message sended to Topic : anmumu is op champion!
a:: got message >> anmumu is op champion!
b:: got message >> anmumu is op champion!
c:: got message >> anmumu is op champion!
*/
~~~
### 옵저버 패턴은 어떻게 구현하나요??
***
여러가지 방법이 있기는 하지만 프록시 객체를 써서 한다.
프록시 객체를 통해 객체의 속성이나 메서드 변화 등을 감지하고 이를 미리 설정해 놓은 옵저버들에게 전달하는 방법으로 구현합니다.
***
###### topic은 주체이자 객체가 됩니다.  
###### implements를 통해 Subject interface를 구현하였고 TopicSubscriber를 통해 옵저버를 선언할 때 해당 이름과 어떤 토픽의 옵저버가 될 것인지 정했다.

자바의 상속과 구현
-
- 상속
  - 상속은 자식 클래스가 부모 클래스의 메서드 등을 상속받아 사용하며 자식 클래스에서 추가 및 확장을 할 수 있는 것을 말한다.
  - 이로 인해 재사용성, 중복성의 최소화가 이루어진다.
- 구현
  - 구현은 부모 인터페이스를 자식 클래스에서 재정의하여 구현 하는 것을 말하며, 상속과는 달리 반드시 부모 클래스의 메서드를 재정의하여 구현해야 한다.

- 차이
  - 상속은 일반 클래스, abstract 클래스를 기반으로 구현하며, 구현은 인터페이스를 기반으로 구현합니다.