# Convert List To Array

`Array` 를 `List` 로 변경한다거나, 반대로 `List` 를 `Array` 로 변경해야 하는 경우는 꽤 많이 있다. 많이 필요한 만큼 방법 또한 다양한데, 문제는 방법이 많은 만큼 헛갈린다는 것! 내가 자신 있게 할 수 있는 방법은 `Loop` 를 사용하는 방법이 유일하지 않을까 싶다. 자주 쓰는 만큼 정리하고 기억하자!

## 개요

`Array` 를 `List` 로 변환하는 방법을 설명한다.

### Loop

반복문을 돌면서 새로 생성한 `Array` 에 값을 추가한다.

```java
List<String> list = new LinkedList<String>();
list.add("Apple");
list.add("Google");
list.add("Microsoft");
list.add("Facebook");

String[] array = new String[list.size()];

for(int = 0; i < list.size(); i++) {
    array[i] = list.get(i);
}
```

### java.util.List

`java.util.List` 인터페이스의  `toArray(T[] a)` 구현체를 사용한다. `toArray` 의 파라미터인 `T[] a` 는 단지 변환하고자 하는 타입을 JVM에 알려 줄 목적으로 사용한다. 다시 말해 크기를 고려하지 않는다.

```java
List<String> list = new LinkedList<String>();
list.add("Apple");
list.add("Google");
list.add("Microsoft");
list.add("Facebook");

String[] array = list.toArray(new String[0])
```

참고 : [toArray의_인자크기](https://stackoverflow.com/questions/174093/toarraynew-myclass0-or-toarraynew-myclassmylist-size)

### Stream

주어진 `List` 를 `Stream` 변환한 다음, `Stream.toArray()` 함수를 이용하여 `List` 의 요소들이 포함 된 `Array` 를 반환 받는다.

#### String Array 생성

```java
List<String> list = new LinkedList<String>();
list.add("Apple");
list.add("Google");
list.add("Microsoft");
list.add("Facebook");

String[] array = list.stream().toArray(String[]::new);
```

#### Primitive Type Int Array 생성

```java
List<Integer> list = new LinkedList<Integer>();
list.add(new Integer(1));
list.add(new Integer(2));
list.add(new Integer(3));
list.add(new Integer(4));

int[] array = list.stream().mapToInt(i -> i.intValue()).toArray();
```



## 참고

https://www.geeksforgeeks.org/list-array-java/

https://www.techiedelight.com/convert-list-to-array-java/