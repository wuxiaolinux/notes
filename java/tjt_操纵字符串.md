
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

## 搜索字符、子串

* `int indexOf(int ch)`

    指定字符第一次出现的索引，如果没有指定的字符，则返回-1

* `int lastIndexOf(int ch)`

    指定字符最后一次出现的索引，如果没有指定的字符，则返回-1

* `int indexOf(int ch, int fromIndex)`

    指定字符第一次出现的索引，从fromIndex往后搜索。

* `int lastIndexOf(int ch, int fromIndex)`

    指定字符最后一次出现的索引，从fromIndex往前搜索。

* `int indexOf(String str)`

    指定字符串第一次出现的索引

* `int lastIndexOf(String str)`

    指定字符串最后一次出现的索引

* `int indexOf(String str, int fromIndex)`

    指定字符串第一次出现的索引，从fromIndex往后搜索。

* `int lastIndexOf(String str, int fromIndex)`

    指定字符串最后一次出现的索引，从fromIndex往前搜索。

* `boolean contains(CharSequence s)`

    查找是否包含指定的字符序列

## 字符、字符串替换

`String`类提供了很少的插入字符和字符串的方法，一般来说，类似的方法是不需要的，你可以这样做：

构造一个新的字符串，通过连接多个子串，这其中一些子串已经从原先的字符串中移除，并使用想插入的子串进行了替换。

> 原文：You can create a new string by concatenation of substrings you have removed from a string with the substring that you want to insert.

在`String`类中提供了4个替换指定字符、字符串的方法：

* `String replace(char oldChar, char newChar)`

    使用字符newChar替换所有的字符oldChar

* `String replace(CharSequence target, CharSequence replacement)`

    使用字符序列replacement替换所有指定字符序列target

* `String replaceAll(String regex, String replacement)`

    使用字符串replacement替换所有符合给定正则表达式的子串

* `String replaceFirst(String regex, String replacement)`

    使用字符串replacement替换第一个符合给定正则表达式的子串

## Example

分隔文件名的不同部分，用到了`lastIndexOf()`方法和`substring()`方法。

代码如下：

```java
public class Filename {
    private String fullPath;
    private char pathSeparator, 
                 extensionSeparator;

    public Filename(String str, char sep, char ext) {
        fullPath = str;
        pathSeparator = sep;
        extensionSeparator = ext;
    }

    public String extension() {
        int dot = fullPath.lastIndexOf(extensionSeparator);
        return fullPath.substring(dot + 1);
    }

    // gets filename without extension
    public String filename() {
        int dot = fullPath.lastIndexOf(extensionSeparator);
        int sep = fullPath.lastIndexOf(pathSeparator);
        return fullPath.substring(sep + 1, dot);
    }

    public String path() {
        int sep = fullPath.lastIndexOf(pathSeparator);
        return fullPath.substring(0, sep);
    }
}
```

构造`Filename`对象，并调用它的方法：

```java
public class FilenameDemo {
    public static void main(String[] args) {
        final String FPATH = "/home/user/index.html";
        Filename myHomePage = new Filename(FPATH, '/', '.');
        System.out.println("Extension = " + myHomePage.extension());
        System.out.println("Filename = " + myHomePage.filename());
        System.out.println("Path = " + myHomePage.path());
    }
}
```
Output is: 

```java
Extension = html
Filename = index
Path = /home/user
```
