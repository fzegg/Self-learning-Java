# Collection子接口

### List接口

- ArrayList、LinkedList、Vector的异同：

  1.相同点：都实现了List接口，存储数据的特点相同：有序、可重复的数据

  2.不同点：

  1）ArrayList：作为List接口的主要实现类，线程不安全，执行效率高；底层使用Object[] elementData存储

```java
//jkd7情况下
ArrayList list  = new ArrayList();//底层创建了长度为10的Object[]数组elementData
list.add(123);//elementData[0] = new Integer(123);
//........
list.add(11);//如果此次添加导致底层数组容量不够，则扩容为原来的1.5倍,同时将原有数组中的数据复制到新的数组中
/*结论：建议开发中使用带参的构造器：
ArrayList list = new Arraylist(int capacity);
*/

//jdk8中的变化：延迟数组创建，节省内存
ArrayList list  = new ArrayList();//底层Object[]数组elementData初始化为{}，没有创建长度为10的数组
list.add(123);//第一次调用add时，才创建长度为10的数组，elementData[0] = new Integer(123);
//........
list.add(11);//后续操作没有差异
```

​		2）LinkedList：对于频繁使用插入删除操作，使用此类效率较高，底层使用双向链表存储

```java
LinkedList list = new LinkedList();//内部声明了Node类型的first和last属性，默认值为null
list.add(123);//将123封装到Node中，创建了Node对象
//其中，Node定义为：体现LinkedList的双向链表的说法
/*
private static class Node<E>{
	E item;
    Node<E> next;
    Node<E> prev;
    
    Node(Node<E> prev, E element, Node<E> next){
    this.item = element;
    this.next = next;
    this.prev = prev;
    }
}
*/

```

​		3）Vector：作为List接口的古老实现类，线程安全，效率低：底层使用Object[] elementData存储

```java
/*
jdk7和jdk8中通过Vector()构造器创建对象时，底层都创建了长度为10的数组；在扩容方面，默认扩容为原来的数组长度的2倍
*/
```

- List接口实现的方法：

```java
public void test(){
	ArrayList list = new ArrayList();
    list.add(123);//void add(int index, Object element)：在index位置插入element元素
    list.add(456);
    list.add("AA");
    list.add(new Person(name:"Tom", age:12));
    list.add(456);
    
    list.add(1, "BB");
    System.out.println(list);
    
    List list1 = Arrays.asList(1, 2, 3);
    list.addAll(list1);//boolean addAll(int index, Collection elements)：从index位置开始将elements中的所有元素都添加进来
    System.out.println(list.size());//9
    
    System.out.println(list.get(1));
    
    int index = list.indexOf(4567);//int indexOf(Object obj)：返回obj在集合中首次出现的位置，如果不存在，返回-1
    System.out.println(index);
    System.out.println(list.lastIndexOf(456));//int lastindexOf(Object obj)：返回obj在集合中末次出现的位置
    
    Object obj = list.remove(index:0);//Object remove(int index)：移除指定index位置的元素，并返回此元素
    System.out.println(obj);
    System.out.println(list);
    
    list.set(1,"CC");//Object set(int index, Object element)：设置指定index位置的元素为element
    System.out.println(list);
    
    List subList = list.subList(2,4);//List subList(int fromIndex, int toIndex)：返回从fromIndex到toIndex位置（左闭右开区间）的子集合
    System.out.println(list);
}
```



### Set接口

- Set：存储无序的、不可重复的数据

  - HashSet：Set的主要实现类，线程不安全；可以存储null值

  ​        1.无序性：不等于随机性。存储的数据在底层数组中并非按照数组索引的顺序添加，而是根据数据的  

  ​			  哈希值决定的。

  ​	    2.不可重复性：保证添加的元素在使用equals()判断时，不能返回true。即相同的元素只能添加一个。

  ​    	3.LinkedHashSet：作为HashSet的子类，遍历其内部数据时，可以按照添加的顺序遍历

     	 	  LinkedHashSet作为HashSet的子类，在添加数据的同时，每个数据还维护了两个引用，记录此数

  ​			  据前一个数据和后一个数据

  - TreeSet：可以按照添加对象的指定属性进行排序

  ​        1.向TreeSet中添加的数据，要求是相同类的对象

  ​        2.两种排序方式：自然排序、定制排序

  ​        3.自然排序中，比较两个对象是否相同的标准为：compareTo()返回0

  ​        4.定制排序中，比较两个对象是否相同的标准为：compare()返回0

- 添加元素的过程：以HashSet为例

  向HashSet中添加元素a，首先调用出a所在类的hashCode()方法，计算元素a的哈希值，此哈希值通过某种算法计算出HashSet底层数组中的存放位置，判断数组此位置上是否已经有元素：

  ​	如果没有其他元素，则添加成功；（1）

  ​	如果有其他元素b（或以链表形式存在的多个元素），则比较a与b的hash值：

  ​		如果哈希值不同，则添加成功。（2）

  ​		如果哈希值相同，需要调用元素a所在类的equals()：

  ​			返回true，添加失败

  ​			返回false，添加成功。（3）

  对于添加成功的（2）（3）而言：元素a与已经在指定索引位置上的数据以链表方式存储（jdk7中将a放到数组中指向原来的元素，jdk8中原来的元素在数组中指向元素a）

- 要求：

  1.向Set中添加的数据，其所在的类一定要重写hashCode()和equals()

  2.重写的hashCode()和equals()尽可能保持一致性：相等的对象必须具有相同的散列码

  3.对象中用作equals()方法比较的Field，都应该用来计算hashCode()



### Map接口

- Map：双列数据，存储key-value对数据

  HashMap：作为Map的主要实现类，线程不安全，效率高；可存储null的key、value

  底层：数组+链表（jdk7） 数组+链表+红黑树（jdk8）

  ​	LinkedHashMap：作为HashMap的子类，保证在遍历Map元素时，可以按照添加的顺序实现遍历。在	原有的底层结构基础上添加了一对指针，指向前一个和后一个。对于频繁的遍历操作执行效率较高。

  TreeMap：保证按照添加的key-value对进行排序，实现排序遍历。此时考虑key的自然排序或定制排序。底层使用红黑树

  HashTable：古老的实现类，线程安全效率低；不能存储null的key、value

- Map结构的理解：

  1.Map中的key：无序的，不可重复的，使用Set存储所有的key ---> key所在的类要重写equals()和hashCode()

  2.Map中的value：无序的，可重复的，使用Collection存储所有的value ---> value所在的类要重写equals()

  3.一个key-value对构成一个Entry对象:

  Map中的entry：无序的，不可重复的，使用Set存储所有的entry

- HashMap的底层实现原理

```java
//jdk7
HashMap map = new HashMap();//实例化以后底层创建了长度为16的一维数组Entry[] table
map.put(key1, value);
//......
//......
/*
首先调用key1所在类的hashCode()计算key1哈希值，经过某种算法计算后得到在Entry数组中存放的位置:
如果如果没有其他元素，则添加成功；（1）
	如果有其他元素b（或以链表形式存在的多个元素），则比较key1与已经存在的一个或多个数据的哈希值：
		如果哈希值不同，则添加成功（2）
		如果哈希值相同，需要调用key1所在类的equals()：
			返回true，使用value1替换value2
			返回false，添加成功（3）
对于添加成功的（2）（3）而言：key1-value1与已经在指定索引位置上的数据以链表方式存储。
在不断的添加过程中，当超出临界值且要存放的位置非空时，默认扩容为原来的两倍，并将原有的数据复制过来。
*/

//jdk8
HashMap map = new HashMap();//此时未创建数组
map.put(key1, value);//底层创建了长度为16的一维数组Node[]
/*
当数组的某一个索引位置上的元素以链表形式存在的数据个数>8且当前数组的长度>64时，此索引位置上的所有数据改为使用红黑树存储
*/
```

- Map的常用方法：

```java
public void test(){
	Map map = new HashMap();//添加
	map.put("AA",123);//Object put(Object key, Object value)：将指定key-value添加到（或修改当前map对象中）
	map.put(45,123);
	map.put("BB" ,56);//修改
	map.put("AA",87);
	System.out.println(map);
	
    Map map1 = new HashMap();
	map1.put("CC",123);
	map1.put("DD",123);
	map.putAll(map1);//void putAll(Map m)：将m中的所有key-value对存放到当前map中
	System.out. printIn(map);//Object remove(0bject key)：移除指定key的key-value对，并返回value
	
    Object value = map.remove( key: "CC");
	System.out.println(value);
	System.out.println(map);//void clear()：清空当前map中的所有数据
	map.clear();
	
    //元素查询的操作
    System.out.printIn(map .size());//int size()：返回map中key-value对的个数
    
    System.out.println(map.get(45));//Object get(Object key)：获取指定key对应的value
	
    boolean isExist = map.containsKey("BB");//boolean containsKey(object key): 是否包含指定的key
    System.out.println(isExist);
    isExist = map.containsValue(123);//boolean containsValue(0bject value): 是否包含指定的value
	//boolean equals(object obj):判断当前map和参数对象obj是否相等
```

