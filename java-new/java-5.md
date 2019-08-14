# Java 5 language enhancements

릴리즈: 2006년 12월 11일

## `JSR 14` [Generics](https://docs.oracle.com/javase/1.5.0/docs/guide/language/generics.html)

콜랙션<sup>`Collection`</sup>에서 엘리먼트<sup>`Element`</sup>를 가져다 사용할 때 캐스트<sup>`cast`</sup>를 해야 했었다.

```java
// Removes 4-letter words from c.
static void expurgate(Collection c) {
    for (Iterator i = c.iterator(); i.hasNext(); ) {
        // Elements must be strings
        if (((String) i.next()).length() == 4) {
            i.remove();
        }
    }
}
```

이 방법은 불편한 것 외에도 안전하지 않다. 컴파일러는 캐스트가 컬렉션 유형과 같은지 확인하지 않으므로 런타임에서 캐스트가 실패할 수 있다.

```java
List list = new ArrayList();
list.add("string"); // ok
list.add(12); // ok
// java.lang.ClassCastException
String s = list.get(1);
```

제네릭<sup>`generic`</sup>을 사용하면 아래와 같다. 제네릭을 사용하는 코드가 더 명확하고 안전해진다. 안전하지 않은 캐스트와 추가 괄호가 제거됐다.

```java
// Removes the 4-letter words from c
static void expurgate(Collection<String> c) {
    for (Iterator<String> i = c.iterator(); i.hasNext(); ) {
        if (i.next().length() == 4) {
            i.remove();
        }
    }
}
```

더 중요한 것은 메소드 스펙의 일부를 주석에서 서명<sup>`signature`</sup>으로 옮겼기 때문에 컴파일 단계에서 에러를 잡아낼 수 있다.

```java
List<String> list = new ArrayList<String>();
list.add("string"); // ok
list.add(12); // compile error
```

이 외에도 제네릭은 더 많은 기능을 제공한다.

* [Generics in the Java Programming Language](https://www.oracle.com/technetwork/java/javase/generics-tutorial-159168.pdf)

## `JSR 201` [Enhanced `for` Loop](https://docs.oracle.com/javase/1.5.0/docs/guide/language/foreach.html)

기존 `for`문은 아래와 같다.

```java
for (int i = 0; i < list.size() ; i++) {
    String s = list.get(i);
    System.out.println(s); 
}
```

```java
// Removes the 4-letter words from c
for (Iterator<String> i = c.iterator(); i.hasNext(); )
    if (i.next().length() == 4) {
        i.remove();
    }
}
```

Java 5 이상부터 지원하는 `for` 문이다.

```java
// Removes 4-letter words from c. Elements must be strings
for (String s : c) {
    if (s.length() == 4) {
        i.remove();
    }
}
```

## `JSR 201` [Autoboxing/Unboxing](https://docs.oracle.com/javase/1.5.0/docs/guide/language/autoboxing.html)

자바의 데이터 타입은 원시형 타입<sup>`primitive type`</sup>과 참조형 타입<sup>`reference type`</sup>이 있다. 원시형 타입을 1:1로 대응하는 참조형 타입을 래퍼 클래스<sup>`wrapper class`</sup>라 한다.

* 원시형 타입: `byte`, `short`, `int`, `long`, `float`, `double`, `boolean` and `char`
* 래퍼 클래스: `Byte`, `Short`, `Int`, `Long`, `Float`, `Double`, `Boolean` and `Char`

![Imgur](https://i.imgur.com/bLtNFvM.png)

원시형 타입을 래퍼 클래스로 변환하는 것을 박싱<sup>`Boxing`</sup>, 래퍼 클래스를 원시형 타입으로 변환하는 것을 언박싱<sup>`Unboxing`</sup>이라고 한다.

```java
Integer integer = new Integer(10); // Boxing
int i = integer.intValue(); // Unboxing
```

Java 5 부터는 박싱과 언박싱이 자동으로 처리한다.

```java
Integer integer = 10; // Auto Boxing
int i = integer; // Auto Unboxing
```

※ 원시형 타입으로만 연산하는 것이 래퍼 타입으로 연산하는 것보다 3배정도 빠르다고 한다.

## `JSR 201` [Typesafe Enums](https://docs.oracle.com/javase/1.5.0/docs/guide/language/enums.html)

다음 기회에...

## `JSR 201` [Varargs](https://docs.oracle.com/javase/1.5.0/docs/guide/language/varargs.html)

가변 인자<sup>`Varargs`</sup>는 필요에 따라 매개변수를 가변적으로 조정할 수 있는 기술이다.

* 인자를 배열로 받아서 처리 했었다

    ```java
    public class MessageFormat {
        public static String format(String pattern, Object[] arguments) {
            return null;    
        }
    }
    ```
    
    ```java
    Object[] arguments = { new Integer(7), new Date(), "a disturbance in the Force" };
    MessageFormat.format("...", arguments);
    ```

* 가변인자를 사용

    ```java
    public class MessageFormat {
        public static String format(String pattern, Object... arguments) {
            return null;    
        }
    } 
    ```
    
    ```java
    // 가변인자를 사용 (배열을 인자로 넣어도 가능)
    MessageFormat.format("...", 7, new Date(), "a disturbance in the Force");
    ```

## `JSR 201` [Static Import](https://docs.oracle.com/javase/1.5.0/docs/guide/language/static-import.html)

```
int i = Math.abs(-3);
```

Java 5 부터는 정적<sup>`static`</sup> 메소드를 더욱 쉽게 사용하기 위해서 `static import`를 지원한다.

```
import static java.lang.Math.abs;
import static java.lang.Math.PI;

int i = abs(PI);
```

```
import static java.lang.Math.*;

int i = abs(PI);
```

## `JSR 175` [Metadata (Annotations)](https://docs.oracle.com/javase/1.5.0/docs/guide/language/annotations.html)

다음 기회에...

## Reference

* https://docs.oracle.com/javase/1.5.0/docs/relnotes/features.html#lang