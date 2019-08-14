# Java 10 language enhancements

릴리즈: 2018년 3월 20일

## `JEP 286` Local-Variable Type Inference

로컬변수 선언을 `var`를 이용하여 기존의 엄격한 타입 선언 방식에서 탈피하여 컴파일러에게 타입을 추론하게할 수 있다.

```java
var list = new ArrayList<String>(); // infers ArrayList<String>
var stream = list.stream(); // infers Stream<String>
```

## copyOf()

`java.util.List`, `java.util.Map` and `java.util.Set` each got a new static method `copyOf(Collection)`.

It returns the **unmodifiable copy** of the given Collection:

```java
var someIntList = List.of(1, 2, 3);
List<Integer> copyList = List.copyOf(someIntList);
copyList.add(4); // java.lang.UnsupportedOperationException
```

## toUnmodifiable*()

```
var someIntList = List.of(1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11);
List<Integer> evenList = someIntList.stream()
        .filter(i -> i % 2 == 0)
        .collect(Collectors.toUnmodifiableList()); // !
// [2, 4, 6, 8, 10]

evenList.add(12); // UnsupportedOperationException
```

## Optional*.orElseThrow()

```java
var someIntList = List.of(1, 3, 5, 7, 9);
Integer firstEven = someIntList.stream()
        .filter(i -> i % 2 == 0)
        .findFirst()
        .orElseThrow(); // NoSuchElementException
```

## Reference

* [Java Language Changes for Java SE 10](https://docs.oracle.com/javase/10/language/toc.htm#JSLAN-GUID-B06D7006-D9F4-42F8-AD21-BF861747EDCF)