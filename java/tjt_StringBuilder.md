StringBuilder
===

StringBuilder与String类类似，但StringBuilder是可变的，而String是不可变的。

如果需要拼接大量字符串，使用StringBuilder会更高效。

## 长度和容量

1. __`length()`__

length()方法返回包含的字符长度。

1. __`capacity()`__

StringBuilder的capacity字段，表示由该对象分配的用于存放字符的空间大小。capacity始终大于等于length，并且根据需要自动扩展。

## 构造器

1. __`StringBuilder()`__<br/>
capacity为16

1. __`StringBuilder(CharSequence cs)`__<br/>
创建一个包含指定字符序列的StringBuilder对象，capacity的大小为cs的长度 + 16

1. __`StringBuilder(int initCapacity)`__<br/>
创建一个StringBuilder对象，初始容量为initCapacity

1. __`StringBuilder(String s)`__<br/>
创建一个StringBuilder对象，初始值为s，`capacity=s.length()+16`

__举例__

```java
// creates empty builder, capacity 16
StringBuilder sb = new StringBuilder();
// adds 9 character string at beginning
sb.append("Greetings");
```

其中，length=9 & capacity=16：

![StringBuilder](http://ww3.sinaimg.cn/mw1024/006e1q8ojw1ez2y9wlo00g30ct02i0so.gif)

## 设置长度和容量

1.   `void setLength(int newLength)` 设置字符序列的长度，如果newLength小于length()的返回值，则多余的字符将被舍弃。如果newLength大于length()，则多余的位置会被置为`'\0'`（见此方法源码）

2. `void ensureCapacity(int minCapacity)` 确保capacity至少为minCapacity


__setLength(int)源码__
```java
public void setLength(int newLength) {
    if (newLength < 0)
        throw new StringIndexOutOfBoundsException(newLength);
    ensureCapacityInternal(newLength);

    if (count < newLength) {
        Arrays.fill(value, count, newLength, '\0');
    }

    count = newLength;
}
```

## StringBuilder提供的操作

### 增

往字符串中新增字符，新增又分为两类：

__append__

* `StringBuilder append(boolean b)`
* `StringBuilder append(char c)`
* `StringBuilder append(char[] str)`
* `StringBuilder append(char[] str, int offset, int len)`
* `StringBuilder append(double d)`
* `StringBuilder append(float f)`
* `StringBuilder append(int i)`
* `StringBuilder append(long lng)`
* `StringBuilder append(Object obj)`
* `StringBuilder append(String s)`

> append可以接受除byte和short外其他6个基本类型。

__insert__

* `StringBuilder insert(int offset, boolean b)`
* `StringBuilder insert(int offset, char c)`
* `StringBuilder insert(int offset, char[] str)`
* `StringBuilder insert(int index, char[] str, int offset, int len)`
* `StringBuilder insert(int offset, double d)`
* `StringBuilder insert(int offset, float f)`
* `StringBuilder insert(int offset, int i)`
* `StringBuilder insert(int offset, long lng)`
* `StringBuilder insert(int offset, Object obj)`
* `StringBuilder insert(int offset, String s)`

> insert可以接受除byte和short外其他6个基本类型。

### 删

从字符串中删除字符

* `StringBuilder delete(int start, int end)`
* `StringBuilder deleteCharAt(int index)`

> 删除索引在闭区间`[start, end-1]`内的字符序列。或者，删除索引为`index`的字符。

### 改

修改字符串中的字符或顺序

* `StringBuilder replace(int start, int end, String s)`
* `void setCharAt(int index, char c)`
* `StringBuilder reverse()`

> * 使用字符串`s`替换索引在闭区间`[start, end-1]`内的字符序列
> * 使用字符`c`替换索引为`index`的字符
> * 将字符序列顺序颠倒

### 其他

`String toString()`

> 返回一个包含了所有字符序列的字符串


## Example

还是一个回文的例子：

```java
public class StringBuilderDemo {
    public static void main(String[] args) {
        String palindrome = "Dot saw I was Tod";
         
        StringBuilder sb = new StringBuilder(palindrome);
        
        sb.reverse();  // reverse it
        
        System.out.println(sb);
    }
}

// output:
// doT saw I was toD
```

在`System.out.println(sb);`中，隐式调用了`sb.toString()`方法。

> **注意：另外还有一个`StringBuffer`类，功能和`StringBuilder`一样，但`StringBuffer`是线程安全的。**

<br/><br/><br/><br/><br/>
