팩토리 패턴
=
팩토리 패턴이란?
-
- 객체를 사용하는 코드에서 객체 생성 부분을 떼어내 추상화한 패턴이자 상속 관계에 있는 두 클래스에서 상위 클래스가 중요한 뼈대를 결정하고, 하위 클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴
- 상위 클래스와 하위 클래스가 분리 되어 있어 느슨한 결합을 가지며 상위 클래스에서는 인스턴스 생성 방식에 대해 전혀 알 필요가 없어 많은 유연성을 갖는다.
- 객체 생성 로직이 떼어져 있기 때문에 코드를 리팩터링하더라도 한 곳만 고칠 수 있게 되어 있어 유지 보수성이 증가  

예제
-

~~~
abstract class Coffee {
    public abstract int getPrice();

    @Override
    public String toString() {
        return "this coffee is " + this.getPrice();
    }
}

class CoffeeFactory {
    public static Coffee getCoffee(String type, int price) {
        if (type.equalsIgnore("Latte")) return new Latte(price);
        if (type.equalsIgnore("Americano)) return new Americano(price);
        return new DefaultCoffee();
    }
}
~~~

~~~
class DefaultCoffee extends Coffee {
    private int price;
    
    public DefaultCoffee(){
        this.price = -1;
    }
    
    @Override
    public int getPrice() {
        return this.price;
    }
}

class Latte extends Coffee {
    private int price;
    
    public Latte (int price) {
        this.price = price;
    }
    
    @Override
    public int getPrice() {
        return this.price;
    }
}

class Americano extends Coffee {
    private int price;
    
    public Americano (int price) {
        this.price = price;
    }
    
    @Override
    public int getPrice() {
        return this.price;
    }
}
~~~

~~~
public class Main {
    public static void main(String[] args) {
        Coffee latte = CoffeeFactory.getCoffee("Latte", 4000);
        Coffee americano = CoffeeFactory.getCoffee("Americano", 3000);
        System.out.println("Latte : " + latte);
        System.out.println("Americano : " + americano);
    }
}
/*
Latte : this coffee is 4000
Americano : this coffee is 3000
*/
~~~

###### 위 코드를 보면 if 문으로 문자열 기반으로 로직이 구성되어 있다. 이 부분을 ENUM or Map 을 이용한다면 if 문을 사용 하지 않고 매핑 할 수 있다.