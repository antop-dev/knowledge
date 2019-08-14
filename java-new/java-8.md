# Java 8 language enhancements

릴리즈: 2014년 3월 18일

## [Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)

![Imgur](https://i.imgur.com/NBLrK7o.png)

Coming Soon...

## Interface Default and Static Methods

인터페이스<sup>`Interface`</sup>에 정적`static` 메소드와 디폴트`default` 메소드를 사용할 수 있다.

```java
public interface Vehicle {
    static String producer() {
        return "N&F Vehicles";
    }

    default String getOverview() {
        return "ATV made by " + producer();
    }
}
```

정적 메소드는 클래스의 정적 메소드 사용법과 같다.

```java
// call static method of interface
String producer = Vehicle.producer();
```



```java
Vehicle vehicle = new VehicleImpl();
String overview = vehicle.getOverview(); // call default method of interface
```

## Optional<T>

![Imgur](https://i.imgur.com/U9MNh8o.png)

Java 8의 [옵셔널](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html)<sup>`Optional<T>`</sup> 클래스는 NPE<sup>`NullPointException`</sup>를 얻을 가능성이있는 상황을 처리하는 데 도움을 준다.

```
public String someMethod(String input) {
    // process...
    return null;
}

String s = someMethod(" antop ");
System.out.println(s.length()); // NPE
```

```
public static Optional<String> someMethod(String input) {
    // process...
    return Optional.ofNullable(null);
}

Optional<String> s = someMethod(" antop ");
s.ifPresent(it -> System.out.println(it.length())); // null safe
```

## Streams

![Imgur](https://i.imgur.com/XToPO4K.jpg)

다음 기회에....

## `JSR310` Date/Time API

날짜와 시간 조작은 자바 개발자를 가장 괴롭히는 고통 포인트중의 하나다. `java.util.Calendar`에 이어 `java.util.Date`는 모든 상황에서 전혀 향상되고 있지 않았다.(심지어 더욱 복잡하게 만들어졌다.)

그래서 Java를 위한 훌륭한 대안 Date/Time API인 [Joda-Time](https://www.joda.org/joda-time/)이 생겼다. Java 8의 새로운 날짜-시간 API<sup>`JSR310`</sup>은 Joda-Time에 의해 큰 영향을 받았고 그것의 장점을 가져왔다.
                                          
## Base64

[java.util.Base64](https://docs.oracle.com/javase/8/docs/api/java/util/Base64.html) 인코딩 지원은 Java 8 표준 라이브러리로 포함되었다

```java
final String text = "Base64 finally in Java 8!";
final String encoded = Base64.getEncoder().encodeToString(text.getBytes(StandardCharsets.UTF_8));
System.out.println(encoded); // QmFzZTY0IGZpbmFsbHkgaW4gSmF2YSA4IQ==
final String decoded = new String(Base64.getDecoder().decode(encoded), StandardCharsets.UTF_8);
System.out.println(decoded); // Base64 finally in Java 8!
```

## Reference

* [What's New in JDK 8 - Oracle](https://www.oracle.com/technetwork/java/javase/8-whats-new-2157071.html)
* [New Features in Java 8 - Baeldung](https://www.baeldung.com/java-8-new-features)
* [Java 8 Features - The ULTIMATE Guide](https://devtrans.tistory.com/entry/Java-8-Features-The-ULTIMATE-Guide)
