



HMSpring 검색

H

홈
1

DM
2

내 활동
3

캔버스
4

더 보기
0

HMSpring














파일 세부정보

java 단위 평가 포트폴리오.md
서성원
어제, 오전 9:35

# ✅ Java 포트폴리오 단위평가
​
---
​
다음은 **Java 포트폴리오 단위평가 문제**입니다. 요구사항에 따라 다음 기술이 반드시 사용되어야 합니다:
​
* **람다식 (Lambda Expression)**
* **제네릭 (Generic)**
* **컬렉션 프레임워크 (Collection API)**
​
---
​
## ✅ 문제: **고객 주문 통계 분석기**
​
당신은 한 전자상거래 회사의 백엔드 개발자입니다. 고객들의 주문 데이터를 분석하여 특정 통계를 반환하는 유틸리티 클래스를 구현해야 합니다.
​
### �� 요구 사항
​
다음 클래스를 정의하고 요구 기능을 구현하시오:
​
---
​
### 1. 클래스 정의
​
#### `Order`
​
```java
public class Order {
    private String customerName;
    private String product;
    private int quantity;
    private double unitPrice;
​
    // 생성자, getter, toString 오버라이딩 구현
}
```
​
---
​
### 2. 제네릭 유틸리티 클래스 정의
​
#### `OrderProcessor<T extends Order>`
​
* 제네릭 타입을 활용해 `Order` 또는 그 하위 타입 처리 가능하도록 구성
* 주요 기능:
​
```java
public class OrderProcessor<T extends Order> {
​
    private List<T> orders;
​
    public OrderProcessor(List<T> orders) {
        this.orders = orders;
    }
​
    // 총 주문 수량 계산
    public int totalQuantity();
​
    // 총 매출액 계산 (quantity * unitPrice)
    public double totalRevenue();
​
    // 고객별 총 주문액 Map<String, Double> 반환
    public Map<String, Double> revenuePerCustomer();
​
    // 단가 기준 정렬된 주문 리스트 반환 (람다 사용)
    public List<T> sortByUnitPriceDesc();
}
```
​
---
​
### ✨ 구현 조건
​
* `List`, `Map`, `Collectors` 등의 Java 컬렉션 사용
* `for` 루프 대신 **Stream API + 람다식**을 최대한 활용
* `OrderProcessor`는 제네릭으로 구현
* 정렬은 람다를 이용하여 `Comparator`로 구현
​
---
​
## �� 예시
​
```java
List<Order> orders = List.of(
    new Order("Alice", "Laptop", 2, 1200.0),
    new Order("Bob", "Mouse", 5, 25.0),
    new Order("Alice", "Keyboard", 1, 75.0),
    new Order("Charlie", "Monitor", 2, 300.0)
);
​
OrderProcessor<Order> processor = new OrderProcessor<>(orders);
​
System.out.println("총 주문 수량: " + processor.totalQuantity()); // 10
System.out.println("총 매출: $" + processor.totalRevenue()); // 1200*2 + 25*5 + 75*1 + 300*2 = 2400 + 125 + 75 + 600 = 3200
System.out.println("고객별 매출: " + processor.revenuePerCustomer());
// {Alice=2550.0, Bob=125.0, Charlie=600.0}
​
processor.sortByUnitPriceDesc().forEach(System.out::println);
```
​
다음에서 공유됨
slack-전체
22시간 전



