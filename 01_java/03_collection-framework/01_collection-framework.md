### collection framework
- 데이터를 효율적으로 처리할 수 있는 표준화된 방법을 제공하는 클래스의 집합
    - 자료구조와, 알고리즘을 구조화하여 클래스로 구현

- 사용법 : 용도에 맞는 interface 구현체 사용

### interface
1) List interface
    - Collection interface 상속
2) Set interface
    - Collection interface 상속
3) Map interface
    - 구조상 차이로 인해 Map interface 별도 정의

![Alt text](img/00_collection.gif)
![Alt text](img/01_collection.png)

### property
1) List<E>
    - `순서 [O]`, `중복 [O]`
    - ex) Vector, ArrayList, LinkedList, Stack, Queue...
2) Set<E>
    - `순서 [X]`, `중복 [X]`
    - ex) HashSet, TreeSet...
3) Map<K, V>
    - Key, Value 한 쌍으로 구성    
    - `순서 [X]`, `Key 중복 [X]`, `Value 중복 [O]`
    - ex) HashMap, TreeMap, HashTable, Properties...
   
### collection class
- collection framework에 속한 interface를 구현한 클래스 → collection class
- Vector, Hashtable 레거시 호환을 위해 남아있다.
- ArrayList, HashMap 으로 사용하는것이 정신건강에 이롭다.