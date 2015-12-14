
Manipulating Characters in a String
===

`String`类有许多方法可以检查字符串的内部，比如查找字符、子串，改变大小写，等等。

## 通过索引获取字符序列和子串

### charAt()

获取指定索引的字符，索引从0开始，例如：

```java
String anotherPalindrome = "Niagara. O roar again!"; 
char aChar = anotherPalindrome.charAt(9);

// aChar 是 O
```

### substring()

* `String substring(int beginIndex, int endIndex)`

    获取一个子串，子串包括的字符是从原字符串beginIndex索引位置开始，到endIndex-1索引位置止。
    > 我的记忆方法是，左闭右开，索引区间为 [beginIndex, endIndex)

* `String substring(int beginIndex)`
    
    获取一个子串，子串包括的字符是从原字符串beginIndex索引位置开始，到原字符串最后一个字符，及length()-1。

    > 我的记忆方法是，抛弃前面的beginIndex个字符！

## 其他常见操作方法

* `String[] split(String regex)`

    先检索由字符串参数（正则表达式）指定的匹配，再根据这个匹配将字符串分割成一个字符串数组。

* `String[] split(String regex, int limit)`

    和前一个方法一样，但额外限制了分割后字符串数组的最大size

* `CharSequence subSequence(int beginIndex, int endIndex)`

    由字符串的beginIndex索引位置开始，到endIndex-1索引位置为止，构造一个新的字符序列。

* `String trim()`

    构造一个新的字符串，去除原字符串两端的空白符

* `String toLowerCase()`

    将原字符串的字符串全部转换为小写形式，并由此构造一个新的字符串

* `String toUpperCase()`

    将原字符串的字符串全部转换为大写形式，并由此构造一个新的字符串

