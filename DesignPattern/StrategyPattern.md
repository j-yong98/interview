전략 패턴 (Strategy Pattern)
=
전략 패턴이란?
-
- 정책 패턴이라고도 하며, 객체의 행위를 바꾸고 싶은 경우 '직접' 수정하지 않고 전략이라고 부르는 '캡슐화한 알고리즘'을 컨텍스트 안에서 바꿔주면서 상호 교체가 가능하게 만드는 패턴
- 예를 들면, 물건을 구매할 때 네이버페이, 카카오페이 등 여러가지 방법으로 결제하듯 어떤 물건을 살 때 결제 방식의 '전략'만 바꾸는 것을 말합니다.


예제
-

~~~
interface PaymentStrategy {
    public void pay(int amount);
}

class KAKAOCardStrategy implements PaymentStrategy {
    private String name;
    private String cardNumber;
    private String cvv;
    private String dateOfExpiry;

    public KAKAOCardStrategy (String nm, String ccNum, String cvv, String expiryDate) {
        this.name = nm;
        this.cardNumber = ccNum;
        this.cvv = cvv;
        this.dateOfExpiry = expiryDate;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using KAKAOCard.");
    }
}

class LUNACardStrategy implements PaymentStrategy {
    private String emailId;
    private String password;

    public LUNACardStrategy(String email, String pwd) {
        this.emailId = email;
        this.password = pwd;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + " paid using LUNACard.");
    }
}
~~~

~~~
class Item {
    private String name;
    private int price;

    public Item(String name, int cost) {
        this.name = name;
        this.price = cost;
    }

    public String getName() {
        return name;
    }

    public int getPrice() {
        return price;
    }
}

class ShoppingCart {
    List<Item> items;

    public ShoppingCart() {
        this.items = new ArrayList<Item>();
    }

    public void addItem(Item item) {
        this.items.add(item);
    }

    public void removeItem(Item item) {
        this.items.remove(item);
    }

    public int calculateTotal() {
        int sum = 0; 
        for (Item item : items) {
          sum += item.getPrice();
        }
        return sum;
    }

    public void pay (PaymentStrategy paymentMethod) {
        int amount = calcuateTotal();
        paymentMethod.pay(amount);
    }
 }
~~~

~~~
public class Main {
    public static void main (String[] args) {
        ShoppingCart cart = new ShoppingCart();

        Item A = new Item("A", 100);
        Item B = new Item("B", 300);

        cart.addItem(A);
        cart.addItem(B);

        cart.pay(new LUNACardStrategy("abc@abc.com", "1234"));

        cart.pay(new KAKAOCardStrategy("abc", "123456789", "123. "12/12"));
    }
}
/*
400 paid using LUNACard.
400 paid using KAKAOCard.
*/
~~~

###### 전략 패턴을 활용한 라이브러리 예시로 passport라이브러리가 있다.  
###### passport는 인증 모듈을 구현할 때 쓰는 미들웨어 라이브러리로, 여러가지 '전략'을 기반으로 인증할 수 있게 된다.
