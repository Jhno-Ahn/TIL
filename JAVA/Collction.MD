# 컬렉션 프레임웍

- ‘데이터 군을 저장하는 클래스들을 표준화한 설계’ 즉, 표준화된 프로그래밍 방식을 의미

## 컬렉션 프레임웍의 핵심 인터페이스

| 인터페이스 | 특징 |
| --- | --- |
| List | 순서가 있는 데이터의 집합. 데이터의 중복을 허용 (ArrayList, LinkedList, Stack, Vector 등) |
| Set | 순서를 유지하지 않는 데이터의 집합. 데이터의 중복을 허용하지 않는다. (HashSet, TreeSet 등) |
| Map | 키(key)와 값(value)의 쌍(pair)으로 이루어진 데이터의 집합. 순서는 유지되지 않으며, 키는 중복을 허용하지 않고, 값은 중복을 허용한다. (HashMap, TreeMap, Hashtable, Properies 등) |

### Collection 인터페이스

- List와 Set의 조상인 Collection 인터페이스에는 다음과 같은 메서드들이 정의되어 있다.
- 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 가장 기본적인 메서드 다룸

| boolean add(Object o), boolean addAll(Collection  c) | 지정된 객체(o) 또는 Collection(c)의 객체들을 Collection에 추가한다. |
| --- | --- |
| void clear() | Collection의 모든 객체를 삭제한다 |
| boolean contains(Object o) boolean containsAll(Collection c) | 지정된 객체(o) 또는 Collection의 객체들이 Collection에 포함되어 있는지 확인한다. |
| boolean equals(Object o) | 동일한 Collection인지 비교한다. |
| int hashCode() | Collection의 hash code를 반환한다. |
| boolean isEmpty() | Collection이 비어있는지 확인한다. |
| lterator iterator() | Collection의 lterator를 얻어서 반환한다. |
| boolean remove(Object O) | 지정된 객체를 삭제한다. |
| boolean removeAll(Collection c) | 지정된 Collection에 포함된 객체들을 삭제한다. |
| boolean retailAll(Collection c) | 지정된Collection에 포함된 객체만을 남기고 다른 객체들은 Collection에서 삭제한다. 이 작업으로 인해 Collection에 변화가 있으면 true, 그렇지 않으면 false를 반환한다. |
| int size() | Collection에 저장된 객체의 개수를 반환한다. |
| Object[] toArray() | Collection에 저장된 객체를 객체배열로(Object[])로 반환한다. |
| Object[] toArray(Object[] a) | 지정된 배열에 Collection의 객체를 저장해서 반환한다. |

### List 인터페이스

- List인터페이스는 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현

| 메서드 | 설명 |
| --- | --- |
| void add(int index, Object element) boolean addAll(int index, Collection c) | 지정된 위치(index)에 객체 또는 컬렉션에 포함된 객체들을 추가한다. |
| Object get(int index) | 지정된 위치(index)에 있는 객체들을 반환한다.(List의 첫번째 요소부터 순방향으로 찾는다. |
| int indexOf(Object o) | 지정된 객체의 위치(index)를 반환한다. (List의 마지막 요솝터 역방향으로 찾는다.) |
| ListIterator listIterator()                ListIterator listIterator(int index) | List의  객체에 접근할 수 있는 ListIterator를 반환한다. |
| Object remove(int index) | 지정된 위치(index)에 있는 객체를 삭제하고 삭제된 객체를 반환한다. |
| Object set(int index, Object element) | 지정된 위치에 객체를 저장 |
| void sort(Comparator c) | 지정된 비교자(comparator)로 List를 정렬한다, |
| List subList(int fromIndex, int tolndex) | 지정된 벙위(fromIndex부터 toIndex)에 있는 객체를 반환한다. |

### Set 인터페이스

- Set 인터페이스는 중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용
- HashSet, TreeSet 등이 있다.

### Map 인터페이스

- Map인터페이스는 키(key)와 값(value)을 하나의 쌍으로 묶어서 저장
- 키는 중복될 수 없지만 값은 중복 허용
- Hashtable, HashMap, LinkedHashMap, SortedMap, TreeMap 등이 있다.
- values()에서는 반환타입 Collection, keySet()에서는 Set이 반환타입.
- Map인터페이스에서는 값은 중복허용이기 때문에 Collection으로 반환하고, 키는 중복을 허용하지 않기 때문에 Set타입으로 반환.

| 메서드 | 설명 |
| --- | --- |
| void clear() | Map의 모든 객체를 삭제한다. |
| boolean containsKey(Object key) | 지정된 key객체와 일치하는 Map의 Key객체가 있는지 확인한다. |
| boolean containsValue(Object value) | 지정된 value객체와 일치하는 Map의 value객체가 있는지 확인한다. |
| Set entrySet() | Map에 저장되어 있는 key-value쌍을 Map.Entry타입의 객체로 저장한 Set으로 반환한다. |
| boolean equals(Object o) | 동일한 Map인지 비교한다. |
| Object get(Object key) | 지정한 key객체에 대응하는 value객체를 찾아서 반환. |
| int hashCode() | 해쉬코드 반환 |
| boolean isEmpty() | Map이 비어있는지 확인 |
| Set keySet() | Map에 저장되어 있는 모든 key객체 반환 |
| Object put(Object key, Object value) | Map에 value객체를 key객체에 연결(mapping)하여 저장 |
| void putAll(Map t) | 지정된 Map의 모든 key-value)쌍을 추가한다. |
| Object remove(Object key) | 지정한 key객체와 일치하는 key-value객체를 삭제한다. |
| int size() | Map에 저장된 key-value쌍의 개수를 반환한다. |
| Collection values() | Map에 저장된 모든 value객체를 반환한다. |

### Map.Entry 인터페이스

- Map인터페이스의 내부 인터페이스이다.
- 인터페이스도 내부 클래스와 같이 내부 인터페이스 정의 가능
- key-value쌍을 다루기 위해 내부적으로 정의
- Map인터페이스를 구현하는 클래스에서는 Map.Entry인터페이스도 함께 구현해야 한다.

| 메서드 | 설명 |
| --- | --- |
| boolean equals(Object o) | 동일한 Entry인지 비교한다. |
| Object getKey() | Entry의 key객체를 반환한다. |
| Object getValue() | Entry의 value객체를 반환한다. |
| int hashCode() | Entry의 해시코드를 반환한다. |
| Object setValue(Object value) | Entry의 value객체를 지정된 객체로 바꾼다. |
