# Java7 language enhancements

릴리즈: 2011년 7월 28일

## [Binary Literals](https://docs.oracle.com/javase/7/docs/technotes/guides/language/binary-literals.html)

정수형 타입(`byte`, `short`, `int`, `long`)의 상수를 표기할 때 바이너리 표기법을 지원한다. 이때 `0b` 또는 `0B` prefix를 함께 기술합니다.

 ```java
// An 8-bit 'byte' value:
byte aByte = (byte)0b00100001;

// A 16-bit 'short' value:
short aShort = (short)0b1010000101000101;

// Some 32-bit 'int' values:
int anInt1 = 0b10100001010001011010000101000101;
int anInt2 = 0b101;
int anInt3 = 0B101; // The B can be upper or lower case.
```

바이너리 표기법은 데이터의 비트패턴을 좀 더 명확하게 보여주는 장점이 있다.

```java
public static final int[] phases = {
    0x31, 0x62, 0xC4, 0x89, 0x13, 0x26, 0x4C, 0x98
}
```

```java
public static final int[] phases = {
  0b00110001,
  0b01100010,
  0b11000100,
  0b10001001,
  0b00010011,
  0b00100110,
  0b01001100,
  0b10011000
}
```

## [Underscores in Numeric Literals](https://docs.oracle.com/javase/7/docs/technotes/guides/language/underscores-literals.html)

자바7 이후 버전부터 `_`는 숫자 리터럴의 어디에도 등장할 수 있다. 이로 인해 숫자를 끊어 읽을 수 있게 되어 가독성을 향상 시킬 수 있다

```java
int money = 1800000000; // ?
int won = 1_800_000_000; // ok
```

## [Strings in switch Statements](https://docs.oracle.com/javase/7/docs/technotes/guides/language/strings-switch.html)

`switch`문의 식<sup>`expression`</sup>에 `char`, `byte`, `short`, `int`, `Character`, `Byte`, `Short`, `Integer`, `String`, `enum` 타입이 올 수 있으며, 기존에 허용되지 않던 `String` 타입이 추가되었다.

```java
String str = "...";
switch (str) {
    case "bob":
    case "sam":
        //do something ...
        break;
    case "carl":
    case "joy":
        //do something ...
        break;
    case "anna":
    case "haron":
        //do something ...
        break;
    default:
        //do something ...
}
```

## [Type Inference for Generic Instance Creation](https://docs.oracle.com/javase/7/docs/technotes/guides/language/type-inference-generic-instance-creation.html)

```java
Map<String, List<String>> map = new HashMap<String, List<String>>();
```

컴파일러가 컨텍스트에서 인자의 유형을 유추할 수 있다면 생성자 부분에서는 생략이 가능하다. 이 꺽쇠 쌍괄호`<>`을 비공식적으로 다이아몬드<sup>`diamond`</sup>라고 한다.

```java
Map<String, List<String>> map = new HashMap<>();
```

아래와 같이 다이아몬드를 사용하지 않으면 `HashMap` 자체의 타입이 되므로 컴파일러는 경고하게 된다.

```java
Map<String, List<String>> map = new HashMap(); // unchecked conversion warning
```

## [Improved Compiler Warnings and Errors When Using Non-Reifiable Formal Parameters with Varargs Methods](https://docs.oracle.com/javase/7/docs/technotes/guides/language/non-reifiable-varargs.html)

* Heap Pollution
* Variable Arguments Methods and Non-Reifiable Formal Parameters
* Potential Vulnerabilities of Varargs Methods with Non-Reifiable Formal Parameters
* Suppressing Warnings from Varargs Methods with Non-Reifiable Formal Parameters

## [The `try-with-resources` Statement](https://docs.oracle.com/javase/7/docs/technotes/guides/language/try-with-resources.html)

```java
public class FileUtils {
 
    public static String readFirstLineFromFile(String path) {
        BufferedReader br = new BufferedReader(new FileReader(path));
        try {
            return br.readLine();
        } finally {
            if (br != null) {
                br.close();
            }
        }
    }
}
```

`java.lang.AutoCloseable` 인터페이스를 구현한 객체는 `try-with-resources statement`에 의해 자동으로 `close`를 보장한다. 

```java
public class FileUtils {

    public static String readFirstLineFromFile(String path) throws IOException {
        try (BufferedReader br = new BufferedReader(new FileReader(path))) {
            return br.readLine();
        }
    }

}
```

![Imgur](https://i.imgur.com/QlPVLgg.png)

## [https://docs.oracle.com/javase/7/docs/technotes/guides/language/catch-multiple.html](https://docs.oracle.com/javase/7/docs/technotes/guides/language/catch-multiple.html)

## NIO.2

* [File I/O (Featuring NIO.2)](https://docs.oracle.com/javase/tutorial/essential/io/fileio.html)
* [java.nio.file.Path](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html)

## Reference

* https://docs.oracle.com/javase/7/docs/technotes/guides/language/enhancements.html#javase7