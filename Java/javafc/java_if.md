# 조건문

```java
public class IfApp {
 
    public static void main(String[] args) {
 
        boolean sunny = false;
        boolean cloudy = true;

        if(sunny){
            System.out.println("날씨 좋다"); // sunny가 false 이므로 넘어간다
        } else if(cloudy) {
            System.out.println("우중충하네"); // cloudy가 true 이므로 실행한다
        } else {
            System.out.println("나가지 말자");
        }
 
    }
 
}
```
- `if문`은 참과 거짓을 판단하여 코드를 실행한다

