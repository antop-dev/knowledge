# Java 11 language enhancements

릴리즈: 2018년 9월 25일

## `JEP 330` Launch Single-File Source-Code Programs

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

```shell
java HelloWorld.java
```

## `JEP 321` HTTP Client (Standard)

jdk 9에서 추가되고 jdk 10에서 업데이트 된 java.incubator.http 패키지가 인큐베이터에서 나와 `java.net.http` 패키지로 표준화되었다.
 
이 패키지가 개발된 이유는 아래와 같다.

* 베이스가 되는 URLConnection API가 현재는 거의 사용되지 않는 프로토콜을 염두에 두고 설계되었음
* `HTTP/1.1` 보다 너무 추상적임
* 문서화가 잘 되어있지 않아 사용하기 어려움
* Blocking 형태로만 작동
* 유지보수의 어려움

java.net.http로 옮겨진 패키지의 기능은 아래와 같다.

* Non-Blocking request and response 지원 (with CompletableFuture)
* Backpressure 지원(`java.util.concurrent.Flow` 패키지를 통해 RX Flow를 구현체에 적용)
* `HTTP/2` 지원
* Factory method 형태로 지원

## java.lang.String

* boolean [isBlank](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#isBlank())(): 문자열이 비어 있는지 여부를 리턴

    ```java
    String s = "           ";
    System.out.println(s.isBlank()); // true
    ```

* Stream&lt;String&gt; [lines](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#lines())(): 행 구분자<sup>`line separator`</sup>로 구분하여 스트림을 리턴

    ```java
    String s = "corba\n" +
            "transaction\n" +
            "activation\n" +
            "xml.bind\n" +
            "xml.ws\n" +
            "xml.ws.annotation";

    var lines = s.lines().collect(Collectors.toList());
    // [corba, transaction, activation, xml.bind, xml.ws, xml.ws.annotation]
    ```

* String [repeat](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#repeat(int))(int): 값이 문자열의 반복 횟수로 연결된 문자열을 리턴

    ```java
    String s = "a";
    String repeat = s.repeat(4);
    ```

* String [strip](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#strip())(): 앞뒤 공백 제거

    ```java
    Character c = '\u2000';
    String s = c+  "  a  " + c;

    System.out.println("'" + s.trim() + "'"); // '   a   '
    System.out.println("'" + s.strip() + "'"); // 'a'
    ```

* String [stripLeading](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#stripLeading())(): 모든 선행 공백이 제거 된 값이이 문자열 인 문자열을 반환합니다.

    ```java
    Character c = '\u2000';
    String s = c+  "  a  " + c;

    System.out.println("'" + s.stripLeading() + "'");
    // 'a   '
    ```

* String [stripTrailing](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html#stripTrailing())(): 모든 후행 공백이 제거 된 값이이 문자열 인 문자열을 반환합니다.

    ```java
    Character c = '\u2000';
    String s = c+  "  a  " + c;

    System.out.println("'" + s. stripTrailing() + "'");
    // '   a'
    ```

## Reading/Writing Strings to and from the Files

문자열<sup>`String`</sup>을 파일로 쉽게 읽고 쓸 수 있다.

```java
Path path = Files.writeString(Files.createTempFile("test", ".txt"), "This was posted on JD");
System.out.println(path);
String s = Files.readString(path);
System.out.println(s); //This was posted on JD
```

## Reference

* [Java 11 Single File Source Code](https://www.baeldung.com/java-single-file-source-code)
* [90 New Features and APIs in JDK 11 (Part 1)](https://dzone.com/articles/90-new-features-and-apis-in-jdk-11)
* [Big things in JDK 11](https://meetup.toast.com/posts/171)

