# Convert Int Array To List

알고리즘 사이트 문제를 푸는데, `int[]` 를 `List` 로 변환하여 사용해야 할 필요가 생겼다. 습관적으로 `Arrays.asList` 를 사용했는데 결과가 마음 같지 않다. `List<Integer>` 를 반환하는 것이 아니라,  `List<Int[]>`를 반환한다. 전에는 그냥 했는데 하며 구글링 해보니 결국, Apache Common lang에서 제공하는 `ArrayUtils.toObject()` 함수를 먼저 사용했어야 했다. 아무 생각없이 `ctrl+c` 와 `ctrl+v` 를 번갈아가며 개발했던 나의 무지함이 드러나 낯부끄러웠던 순간이었다.

## 개요

`int[]` 를 `List<Integer>` 로 변환하는 방법을 설명한다.

### Naive

반복문을 돌면서 생성한 `List` 에 값을 추가한다.

```java
int[] intArray = {1,2,3,4,5};
List<Integer> arrayList = new ArrayList<Integer>();

for( int i : intArray) {
    arrayList.add(i);
}
```

### Java 8

Stream API를 이용하여 `List<Integer>` 생성한다.

```java
int[] intArray = {1,2,3,4,5};
List<Integer> arrayList =Arrays.Stream(intArray).boxed().collect(Collectors.toList());
```

### Apache Common lang

```java
int[] intArray = {1,2,3,4,5};
List<Integer> arrayList = Arrays.asList(ArrayUtils.toOgject(intArray));
```

## 참고

https://stackoverflow.com/questions/1073919/how-to-convert-int-into-listinteger-in-java
