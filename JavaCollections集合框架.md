# JavaCollections框架是什么  

Java Collections框架中包含了大量集合接口以及这些接口的实现类和操作这些类的算法（比如排序、查找、反转、替换等）。其中Collection是整个集合框架的基础，里面存储一组对象，作用只是提供维护一组对象的基本接口而已。   

- Collection
    - Set 
        - HashSet
        - LinkHashSet
        - TreeSet
    - List
        - ArrayList
        - LinkedList
        - Vector
- Map 
    + HashMap
    + LinkedHashMap
    + TreeMap

### **Set** 
Set是一种不包含重复元素的Collection。允许null的存在，但是只能有一个。所有传入Set中的元素都必须不同。

#### HashSet、LinkedHashSet、TreeSet比较 
**HashSet：**

- 不能保证元素的排列顺序
- 线程非安全即不是同步的  

当向集合中添加元素的时候，HashSet会调用该对象的hashCode()方法得到该对象的hashCode值，然后根据hashCode值来决定该对象在HashSet中的存储位置。
**注：**如果要把一个对象放入HashSet中，重写该对象对应类的equals方法，也应该重写其hashCode()方法。其规则是如果两个对象通过equals方法比较返回true时，其hashCode也应该相同。  

**LinkedHashSet**  

同样是根据hashCode来决定元素的存储位置，但是同时使用链表维护元素的次序，也就是说，当遍历集合时，LinkedHashSet将会以元素的添加顺序访问集合的元素。

**TreeSet**

TreeSet是SortedSet接口的唯一实现类，可以确保集合元素处于排序状态。支持两种排序方式：自然排序和定制排序。其中自然排序为默认的排序方式。  

自然排序：自然排序使用要排序元素的CompareTo（Object obj）方法来比较元素之间大小关系，然后将元素按照升序排列。Java提供了一个Comparable接口，该接口里定义了一个compareTo(Object obj)方法，该方法返回一个整数值，实现了该接口的对象就可以比较大小。obj1.compareTo(obj2)方法如果返回0，则说明被比较的两个对象相等，如果返回一个正数，则表明obj1大于obj2，如果是负数，则表明obj1小于obj2。如果我们将两个对象的equals方法总是返回true，则这两个对象的compareTo方法返回应该返回0。  

定制排序  
自然排序是根据集合元素的大小，以升序排列，如果要定制排序，应该使用Comparator接口，实现 int compare(T o1,T o2)方法。

### **List** 

List集合代表一个有序集合，集合中每个元素都有对应的顺序索引，允许重复元素，可以通过索引来访问指定位置的集合元素。

#### ArrayList、Vector、LinkedList比较

ArrayList和Vector都是基于存储元素的Object[] array来实现的，会在内存中开辟连续的空间来存储。索引速度快，但是插入元素时由于需要移动容器中的元素位置，所以插入操作比较慢。 
两者的最大区别就是Vector是线程安全的，但是现在已经基本不用Vector了。

LinkedList是采用双向链表来实现的，对数据的索引需要从列表头开始遍历，因此查询比较慢，但是插入删除的操作比较快。

### Map 

Map由一系列键值对组成，提供了key到Value的映射。在Map中应保持key与Value的一一对应关系，也就是一个key对应一个Value，因此不能存在相同的key值，但是可以存在相同的Value值。

#### HashMap、LinkedHashMap、TreeMap的比较

Hashmap 是一个最常用的Map，它根据键的HashCode 值存储数据，根据键可以直接获取它的值，具有很快的访问速度。遍历时，取得数据的顺序是完全随机的。HashMap最多只允许一条记录的键为Null;允许多条记录的值为Null;HashMap不支持线程的同步，即任一时刻可以有多个线程同时写HashMap;可能会导致数据的不一致。如果需要同步，可以用Collections的synchronizedMap方法使HashMap具有同步的能力。  

Hashtable 与 HashMap类似，不同的是:它不允许记录的键或者值为空;它支持线程的同步，即任一时刻只有一个线程能写Hashtable，因此也导致了Hashtale在写入时会比较慢。  

LinkedHashMap保存了记录的插入顺序，在用Iterator遍历LinkedHashMap时，先得到的记录肯定是先插入的，也可以在构造时用带参数，按照应用次数排序。在遍历的时候会比HashMap慢，不过有种情况例外，当HashMap容量很大，实际数据较少时，遍历起来可能会比LinkedHashMap慢，因为LinkedHashMap的遍历速度只和实际数据有关，和容量无关，而HashMap的遍历速度和他的容量有关。如果需要输出的顺序和输入的相同，那么用LinkedHashMap可以实现，它还可以按读取顺序来排列，像连接池中可以应用。LinkedHashMap实现与HashMap的不同之处在于，后者维护着一个运行于所有条目的双重链表。此链接列表定义了迭代顺序，该迭代顺序可以是插入顺序或者是访问顺序。对于LinkedHashMap而言，它继承与HashMap、底层使用哈希表与双向链表来保存所有元素。其基本操作与父类HashMap相似，它通过重写父类相关的方法，来实现自己的链接列表特性。  

TreeMap实现SortMap接口，内部实现是红黑树。能够把它保存的记录根据键排序，默认是按键值的升序排序，也可以指定排序的比较器，当用Iterator 遍历TreeMap时，得到的记录是排过序的。TreeMap不允许key的值为null。非同步的。 

一般情况下，我们用的最多的是HashMap，HashMap里面存入的键值对在取出的时候是随机的，它根据键的HashCode值存储数据，根据键可以直接获取它的值，具有很快的访问速度。在Map 中插入、删除和定位元素，HashMap 是最好的选择。
TreeMap取出来的是排序后的键值对。但如果您要按自然顺序或自定义顺序遍历键，那么TreeMap会更好。
LinkedHashMap 是HashMap的一个子类，如果需要输出的顺序和输入的相同，那么用LinkedHashMap可以实现，它还可以按读取顺序来排列，像连接池中可以应用。

