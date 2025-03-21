#### Map
- 중복되는 필드가 있는가 ex) table, category
		- Key를 Enum으로 정의할 수 있는가   ex) category
			- Enum을 사용하라  
- 중복된 필드를 key로 하고 value를 List<Order.>의 형태가 가능한가?
- key로 조회를 많이 해야하나?
---

만약 단순하게 [상품-수량.]의 관계라면 Order객체를 생성하고 Cart에 List<Order.>로 관리하는게 좋다.

하지만 공통적으로 많이 가지는 큰 틀이 있다면, 예를들어 치킨집 포스의 Table 같은, 그럼 Map의 사용을 고려해볼 만 하다.

치킨집 포스를 Order에 Table 필드를 정의할 경우에는 다음과 같은 형태가 된다.
```java
public class Order {  
    private final Table table;  
    private final Map<Menu, Integer> order;
```

```java
public class Cart {  
    private final List<Order>
```

Table은 한정적이고, 다른 Order에도 범용적으로 사용될 수 있다는 것을 볼 수 있다.
그럼 Table를 상위 객체로 뺴면 된다.

- Table은 수량이 적고 한정적이지만 주문에 필수적인 객체다. => 중복 절감
- 메뉴 이름과 수량도 주문에 필수적이지만, 주문마다 다를 확률이 크다.
- Table로 조회하는 경우가 많다
-> Table를 key로한 Map을 사용한다.


#### 개선된 자료형
```java
public class Order {  
    private final Menu menu;  
    private int quantity;
```

```java
public class Cart {  
    private final Map<Table, List<Order>> orders;
```
