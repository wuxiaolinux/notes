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

1.   `void setLength(int newLength)` 设置字符序列的长度，如果newLength小于length()的返回值，则多余的字符将被舍弃。如果newLength大于length()，则多余的位置会被置为`'\0'`，源码：   

        ::java
        public void setLength(int newLength) {
            if (newLength < 0)
                throw new StringIndexOutOfBoundsException(newLength);
            ensureCapacityInternal(newLength);

            if (count < newLength) {
                Arrays.fill(value, count, newLength, '\0');
            }

            count = newLength;
        }

2. `void ensureCapacity(int minCapacity)` 确保capacity至少为minCapacity

