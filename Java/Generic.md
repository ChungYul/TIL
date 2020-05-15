# Generic

## [Generics, Inheritance, and Subtypes][1]

`Box<T>`  클래스에서 `Box<Integer>`와  `Box<Number>` 는 아무런 관계(Relationship)가 없다.

`Box<Integer>` is not a subtype of `Box<Number>` even though `Integer` is a subtype of `Number`

## [Wildcards][2]

Question Mark는 Wildcard라고 부른다.

### Upper Bounded Wildcards

`List<Integer>` , `List<Double>` , `List<Number>` 가 작동하는 프로그램을 작성하고 싶으면, upper bounded wildcard를 사용할 수 있다.

upper bound wildcard를 정의하기 위해 '?' 에 뒤따라 `extends` 키워드를 사용한다.

위 예제를 위해 `List<? extends Number>` 를 사용한다.

list의 합을 계산하는 sumOfList 함수를 만들어 보자.

```java
public static doublc sumOfList( List<? extends Number>) {
    double s = 0.0;
    for ( Number n : list ) {
        s += n.doubleValue();
    }
    return s;
}
```

아래의 코드는 `Integer` 객체를 이용하고 있으며 그 결과로 sum = 6.0 을 얻는다.

```java
List<Integer> li = Arrays.asList(1, 2, 3);
System.out.println("sum = " + sumOfList(li));
```

다음 예제는 `Double` 객체를 사용하며, 동일한 sumOfList 함수를 사용한다. 결과 값으로 sum = 7.0 을 출력한다.

```java
List<Double> ld = Arrays.asList(1.2, 2.3, 3.5);
System.out.println("sum = " + sumOfList(ld));
```

### Unbounded Wildcards

Unbounded Wildcard 타입은 Wildcard 문자 (?) 를 사용한다. 그 사용의 예는  `List<?>` 와 같다.

`printList` 를 생각해 보자. 

```java
public static void printList(List<Object> list) {
    for ( Object elem : list )
        System.out.println(elem+ " ");
    System.out.println();
}
```

이 함수의 목적은 모든 타입의 리스트를 출력하는 것이다. 하지만 그 목적은 달성 될 수 없다.  `printList`  는 단지 `Object` 의 리스트만을 출력하도록 작성되어 있기 때문이다. `List<Integer>` `List<String>` `List<Double>` 은 출력하지 않는다. 그 이유는  `List<Object>`  와 `List<Integer>` `List<String>` `List<Double>`  사이의 상속관계에 있다.

그럼 목적을 달성하기 위해 printList 함수에 Unbounded Wildcards 를 적용해보자.

```java
public static void printList(List<?> list ) {
    for ( Object elem : list )
        System.out.println(elem + " ");
    System.out.println();
}
```

`List<?>` 에는 `null` 을 제외한 어떠한 값도 넣을 수 없다. `List<?>`  는 모든 Generic 리스트의 최상위 타입이기 때문이다.

### Lower Bounded Wildcards

Lower Bound Wildcard는 알지 못하는 Super 타입을 제한한다.

Lower Bound Wildcard는 ('?') 와 super 키워드를 사용하여 정의한다.

`Integer` 와 `Integer` 의 Super 타입인 `Number` , `Object`  로 함수 사용을 제약하고자 한다면,  `<? super Integer>` 를 사용한다.

```java
public static void addNumber ( List<? super Integer> list) {
    for(int i=1; i <= 10; i++) {
        list.add(i);
    }
}
```

### [Wildcards and Subtyping][3]

Generics Class와 Interface 간에는 상속관계가 존재하지 않는다.

A 클래스는 B클래스의 부모관계를 갖는다고 하자.

```java
class A { /*....*/ }
class B extends A { /*....*/ }
```

다음 코드는 일반적이고 정상적이다다.

```java
B b = new B();
A a = b;
```

하지만, Generic Type에서는 A 클래스와 B 클래스의 상속관계가 유효하지 않다.

```java
List<B> lb = new ArrayList<>();
List<A> la = lb; // compile-time error
```

### [Wildcard Capture and Helper Methods][4]

Generics 는 컴파일 타임에 타입을 강제하기 위해 추가되었다. 아래의 코드는 컴파일 에러를 발생시킨다.

```java
import java.util.List;

public class WildcardError {
    
    void foo(List<?> i) {
        i.set(0, i.get(0));
    }
}
```

왜냐면, `foo` 함수가 `List.set(int, E)` 호출할 때, 컴파일러는 리스트에 추가되는 `E` 타입을 모르기 때문이다. Helper 함수를 추가하여 위 상황을 피해 갈 수 있다.

```java
import java.util.List;

public class WildcardFixed {
    
    void foo(List<?> i) {
        fooHelper(i);
    }
    
    // Helper method create so that the wildcard can be captured
    // through type interface
    private <T> void fooHelper(List<T> l) {
        l.set(0, l.get(0));
    }
}
```

### Guideline for Wildcard Use

wildcard 사용을 위한 가이드 라인

- An "in" variable is defined with an upper bounded wildcard, using the `extends` keyword
- An "out" varialbe is defined with a lower bounded wildcard, using the `super` keyword
- In the case where the "in" variable can be accessed using methods defined in the `object` class, use an unboudned wildcard
- In the case where the code needs to access the variable as both an "in" and "out" variable, do not use a wildcard

아래의 코드에서 `ln` 에 `NaturalNumber` 객체를 추가 할 수 없다.  컴파일러는 `List`  에 추가하는 타입의 객체가 무엇인지 확인 할 수 없기 때문이다. 즉, `<? extends NaturalNumber>` 란 거는 알지만 특정 타입 `T` 는 확인 할 수 없다.

```java
class NaturalNumber {
    
    private int i;
    
    public NaturalNumber(int i) { this.i = i; }
    // ...
}

class EvenNumber extends NaturalNUmber {
    public EvenNumber(int i) { super(i); }
}
```

## Type Erasure



[1]: https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html
[2]: https://docs.oracle.com/javase/tutorial/java/generics/wildcards.html
[3]: ttps://docs.oracle.com/javase/tutorial/java/generics/subtyping.html
[4]: https://docs.oracle.com/javase/tutorial/java/generics/capture.html

