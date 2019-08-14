# Java 12 language enhancements

릴리즈: 2019년 3월 19일

## `JEP 325` Switch expressions

```java
int numberOfLetters;

switch (fruit) {
case PEAR:
    numberOfLetters = 4;
    break;
case APPLE:
case GRAPE:
case MANGO:
    numberOfLetters = 5;
    break;
case ORANGE:
case PAPAYA:
    numberOfLetters = 6;
    break;
default:
    throw new IllegalStateException (“Wut” + fruit);
}
```

```java
int numberOfLetters = switch (fruit) {
    case PEAR -> 4;
    case APPLE, MANGO, GRAPE -> 5;
    case ORANGE, PAPAYA -> 6;
    default -> throw new IllegalStateException("Wut " + fruit);
};
```

## Reference

* [39 New Features (and APIs) in JDK 12](https://www.azul.com/39-new-features-and-apis-in-jdk-12/)
* [Java 12: New Features and Enhancements Developers Should Know](https://stackify.com/java-12-new-features-and-enhancements-developers-should-know/)
