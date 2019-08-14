# Java 9 language enhancements

릴리즈: 2017년 9월 21일

## Modular System – Jigsaw Project

[Project Jigsaw: Module System Quick-Start Guide](http://openjdk.java.net/projects/jigsaw/quick-start)

## Private interface methods

```java
public interface MyInterface {

    void normalInterfaceMethod();

    default void interfaceMethodWithDefault() {
        init();
    }

    default void anotherDefaultMethod() {
        init();
    }

    // This method is not part of the public API exposed by MyInterface
    private void init() {
        System.out.println("Initializing");
    }

}
```

## Try-With-Resources

`try`문 안에 새 변수를 선언하지 않아도 자원을 관리할 수 있다.

```java
MyAutoCloseable mac = new MyAutoCloseable();
try (mac) {
    // do some stuff with mac
}
```

## Immutable Set

불변 컬랙션을 만드는 API가 추가되었다.

```java
Set<String> immutableSet = Set.of("a", "b", "c");
List<String> immutableList = List.of("a", "b", "c");
Map<String, Integer> immutableMap = Map.of("a", 1, "b", 2);
```


## Optional To Stream

`java.util.Optional.stream()` gives us an easy way to you use the power of Streams on Optional elements:

```java
List<Optional<String>> listOfOptionals = List.of(
        Optional.of("a"),
        Optional.empty(),
        Optional.of("b"),
        Optional.of("c"),
        Optional.ofNullable("d"),
        Optional.ofNullable(null)
);

// [a, b, c, d]
List<String> collect = listOfOptionals.stream()
        .flatMap(Optional::stream)
        .collect(Collectors.toList());
```

## Reference

* [Java Language Changes for Java SE 9](https://docs.oracle.com/javase/10/language/toc.htm#JSLAN-GUID-B06D7006-D9F4-42F8-AD21-BF861747EDCF)
* [9 new features in Java 9](https://www.pluralsight.com/blog/software-development/java-9-new-features)