# OpenTutorial App

## 구상

![java_myApp_01](./images/java_myApp_01.png)

판매자로서 무언가를 팔고 세금, 기타 비용등을 제하고 남은 이익을 동업자와 배분하는 상황 가정

## 프로그래밍

```java
public class AccountingApp
{

    public static void main(String[] args)
    {
        System.out.println("Value of supply : " + 10000.0);
        System.out.println("VAT : " + (10000.0 * 0.1));
        System.out.println("Total : " + (10000.0 + 10000.0 * 0.1));
        System.out.println("Expense : " + (10000.0 * 0.3));
        System.out.println("Income : " + (10000.0 - 10000.0 * 0.3));
        System.out.println("Devidend 1 : " + (10000.0 - 10000.0 * 0.3) * 0.5);
        System.out.println("Devidend 2 : " + (10000.0 - 10000.0 * 0.3) * 0.3);
        System.out.println("Devidend 3 : " + (10000.0 - 10000.0 * 0.3) * 0.2);
    }

}
```

- 어떠한 동작을 시간에 순서에 따라 실행되도록 작성

## 변수화

```java

public class AccountingApp
{

    public static void main(String[] args)
    {
        double valueOfSupply = Double.parseDouble(args[0]); // 물건의 가격을 인자로 받아오기
        double vatRate = 0.1;
        double expenseRate = 0.3;
        double vat = valueOfSupply * vatRate;
        double total = valueOfSupply + vat;
        double expense = valueOfSupply * expenseRate;
        double income = valueOfSupply - expense;
        double dividend1 = income * 0.5;
        double dividend2 = income * 0.3;
        double dividend3 = income * 0.2;
 
        System.out.println("Value of supply : " + valueOfSupply);
        System.out.println("VAT : " + vat);
        System.out.println("Total : " + total);
        System.out.println("Expense : " + expense);
        System.out.println("Income : " + income);
        System.out.println("Dividend 1 : " + dividend1);
        System.out.println("Dividend 2 : " + dividend2);
        System.out.println("Dividend 3 : " + dividend3);
    }

}

```

- 동일한 코드를 `변수`로 지정해 `데이터가 변할 때마다 새로 작성하는 수고`를 줄임
- 깔끔하고 간결한 코드는 덤