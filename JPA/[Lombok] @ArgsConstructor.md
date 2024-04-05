# [Lombok] @ArgsConstructor

Lombok은 불필요한 코드와 작업을 줄여주는 좋은 라이브러리지만, 무분별하게 사용하면 코드를 분석하는 입장에서는 혼동이 올지도 모른다.

아래는 생성자를 자동 생성해주는 어노테이션 종류이다.

- `@NoArgsConstructor` : 파라미터가 없는 디폴트 생성자를 생성
- `@AllArgsConstructor` : 모든 필드 값을 파라미터로 받는 생성자를 생성
- `@RequiredArgsConstructor` : `final`이나 `@NonNull`으로 선언된 필드만을 파라미터로 받는 생성자를 생성

## `@NoArgsConstructor`

`@NoArgsConstructor` 어노테이션은 파라미터가 없는 디폴트 생성자를 자동으로 생성한다. 이 어노테이션을 사용하면, 클래스에 명시적으로 선언된 생성자가 없더라도 인스턴스를 생성할 수 있다.

```java
@NoArgsConstructor
public class Person {
    private String name;
    private int age;
    // getters and setters
}
```

NoArgsConstructor를 사용하면 Java 코드는 다음과 같아진다.

```java
public class Person {
    private String name;
    private int age;

	public Person(){}
}
```

## `@AllArgsConstructor`

`@AllArgsConstructor` 어노테이션은 클래스의 모든 필드 값을 파라미터로 받는 생성자를 자동으로 생성한다. 이 어노테이션을 사용하면, 클래스의 모든 필드를 한 번에 초기화할 수 있다.

```java
@AllArgsConstructor
public class Person {
    private String name;
    private int age;
    // getters and setters
}
```

`@AllArgsConstructor` 사용하면 Java 코드는 다음과 같아진다.

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
    	this.name = name;
        this.age = age;
    }
}
```

## `@RequiredArgsConstructor`

`@RequiredArgsConstructor` 어노테이션은 `final`이나 `@NonNull`으로 선언된 필드만을 파라미터로 받는 생성자를 자동으로 생성한다. 이 어노테이션을 사용하면, 클래스가 의존하는 필드를 간단하게 초기화할 수 있다.

```java
@RequiredArgsConstructor
public class Person {
    private final String name;
    private final int age;
    private String address;
    // getters and setters
}
```

`@RequiredArgsConstructor` 사용하면 Java 코드는 다음과 같아진다.

```java
public class Person {
    private final String name;
    private final int age;
    private String address;

	public Person(final String name, final int age) {
    	this.name = name;
        this.age = age;
    }
}
```

그리고 각 어노테이션에 세부 옵션을 지정해줄 수 있다. 아래는 옵션 설명을 한다.

- staticName : 정적 팩토리 메소드를 생성
- access : 접근제한자를 지정
- onConstructor : 생성자의 접근 제어자를 설정, 기본값은 public
- force : final 필드가 선언된 경우 컴파일 타임에 기본값을 0 / null / false 로 설정

## staticName

모든 생성자 어노테이션에 사용될 수 있다. 아래는 AllArgsConstructor 에 옵션을 설정한 예시이다.

```java
@AllArgsConstructor(staticName = "of")
public class Person {
    private String name;
    private int age;
    private String address;
}
```

`@AllArgsConstructor` 에 force 옵션을 사용하면 Java 코드는 다음과 같아진다.

```java
@AllArgsConstructor(staticName = "of")
public class Person {
    private String name;
    private int age;
    private String address;

    public static Person of(String name, int age, String address) {
       return new Person(name, age, address);
    }
}
```

## access

access 옵션엔 다음과 같은 접근제어자가 있다.

- PUBLIC: 기본값이며, 모든 클래스에서 생성자에 접근 가능
- PROTECTED: 같은 패키지의 클래스와 상속받은 클래스에서 생성자에 접근 가능
- PACKAGE: 같은 패키지의 클래스에서 생성자에 접근 가능
- PRIVATE: 해당 클래스 내부에서만 생성자에 접근 가능

이 외에도 NONE과 MODULE 접근 제어자가 있지만, 일반적으로 사용하지 않는다.

## force

`@NoArgsConstructor` 어노테이션에서만 사용이 가능하고 해당 옵션을 지정할경우 primitive type 에 맞는 기본 값이 설정된다.

```java
@NoArgsConstructor(force = true)
public class Person {
    private final String name;
    private final int age;
    private String address;
}
```

`@NoArgsConstructor` 에 force 옵션을 사용하면 Java 코드는 다음과 같아진다.

```java
public class Person {
    private final String name = null;
    private final int age = 0;
    private String address;
}
```

위 3개의 생성자 어노테이션들은 상황에 알맞게 조합해서 사용해야된다.
