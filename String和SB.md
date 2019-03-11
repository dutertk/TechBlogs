### String类
想要了解一个类就是读一个类的源码，虽然我也不太能读的懂
```
public final class String
    implements java.io.Serializable, Comparable<String>, CharSequence
{
    /** The value is used for character storage. */
    private final char value[];
 
    /** The offset is the first index of the storage that is used. */
    private final int offset;
 
    /** The count is the number of characters in the String. */
    private final int count;
 
    /** Cache the hash code for the string */
    private int hash; // Default to 0
 
    /** use serialVersionUID from JDK 1.0.2 for interoperability */
    private static final long serialVersionUID = -6849794470754667710L;
 
    ......
 
}

public String substring(int beginIndex, int endIndex) {
    if (beginIndex < 0) {
        throw new StringIndexOutOfBoundsException(beginIndex);
    }
    if (endIndex > count) {
        throw new StringIndexOutOfBoundsException(endIndex);
    }
    if (beginIndex > endIndex) {
        throw new StringIndexOutOfBoundsException(endIndex - beginIndex);
    }
    return ((beginIndex == 0) && (endIndex == count)) ? this :
        new String(offset + beginIndex, endIndex - beginIndex, value);
    }
 
 public String concat(String str) {
    int otherLen = str.length();
    if (otherLen == 0) {
        return this;
    }
    char buf[] = new char[count + otherLen];
    getChars(0, count, buf, 0);
    str.getChars(0, otherLen, buf, count);
    return new String(0, count + otherLen, buf);
    }
```
从源码中可以看出：   

- String类是final类，并且成员方法都是final来修饰的，所以是不能被继承，也不能修改的。
- string类的操作并不是对原有的字符串上进行的，而是重新生成了一个新的字符串对象。

以String str= "Hello World"和String str = new String("Hello World")为例。   
```

public class Main {
         
    public static void main(String[] args) {
        String str1 = "hello world";
        String str2 = new String("hello world");
        String str3 = "hello world";
        String str4 = new String("hello world");
         
        System.out.println(str1==str2);
        System.out.println(str1==str3);
        System.out.println(str2==str4);
    }
}
```
输出结果是**false，true，false，**这是因为jvm的内存机制会在class文件中存在着一个常量池，str1和str3都在编译旗舰生成了字面常量和符号引用。jvm会在运行时常量池查找是否存在相同的字面常量，如果存在，会直接将引用指向已经存在的字面常量。
### StringBuilder和StringBuffer
这两个类都是在原有对象的基础上进行操作，并且只进行了一次new操作，不会产生新的对象，所占的资源要比
string小   
<font size="4">StringBuilder类中的insert方法</font>
```
public StringBuilder insert(int index, char str[], int offset,
                              int len) 
  {
      super.insert(index, str, offset, len);
  return this;
  }

```
<font size="4">StringBuffer类中的insert方法  </font>
```

public synchronized StringBuffer insert(int index, char str[], int offset,
                                            int len) 
    {
        super.insert(index, str, offset, len);
        return this;
    }
```

从源码中可以看出：StringBuffer的方法加了同步锁，因此跟String类一样都是线程安全的。而StringBuilder则是非线程安全的。
总结：   

1. 操作少量的数据 ->> string
2. 单线程操作字符串缓冲区下大量数据 ->> StringBuilder
3. 多线程操作字符串缓冲区下大量数据 ->> StringBuffer

