Strings
===

字符的序列叫做字符串，在Java中，字符串是对象，对应的类是`String`。

## 创建字符串

```java
// 方式1：使用字面量
String greeting = "Hello world!";

// 方式2：使用构造器（多个构造器）
char[] helloArray = { 'h', 'e', 'l', 'l', 'o', '.' };
String helloString = new String(helloArray);

```

## 字符串长度

`length()`方法返回字符串对象中包括的字符个数，如

```java
String palindrome = "Dot saw I was Tod";
int len = palindrome.length();

// len是17
```

`palindrome`是回文的意思，在诗歌里有这种运用。下面的代码颠倒了字符串的顺序，其中使用到了`charAt(i)`方法：

```java
public class StringDemo {
    public static void main(String[] args) {
        String palindrome = "Dot saw I was Tod";
        int len = palindrome.length();
        char[] tempCharArray = new char[len];
        char[] charArray = new char[len];
        
        // put original string in an 
        // array of chars
        for (int i = 0; i < len; i++) {
            tempCharArray[i] = 
                palindrome.charAt(i);
        } 
        
        // reverse array of chars
        for (int j = 0; j < len; j++) {
            charArray[j] =
                tempCharArray[len - 1 - j];
        }
        
        String reversePalindrome = new String(charArray);
        System.out.println(reversePalindrome);
    }
}

// 输出：doT saw I was toD
```

上面的代码中，第一个循环是将字符串转换为一个字符数组，这里可以使用`getChars()`方法来做：

```java
palindrome.getChars(0, len, tempCharArray, 0);

// 这个方法将对象的一些字符复制到指定的字符数组中
// 第1个参数：被复制的第一个字符的索引
// 第2个参数：被复制的最后一个字符的索引 + 1
// 第3个参数：指定字符数组
// 第4个参数：从这个索引位置开始写入复制出来的字符
```


## 串联字符串

连接两个字符串的方法`string1.concat(string2)`，在string1后连接string2。

连接字符串还可以使用`+`，可以连接2个以上的字符串。

通过`+`操作符，可以连接任何对象，如果对象不是字符串，则自动调用对象的`toString()`方法，将返回的结果字符串进行连接。

`+`操作符还有一个重要的地方，字符串字面量不能跨越在多行，如果有必要，必须使用在每一行的末尾使用`+`来连接。如：

```java
String quote = 
    "Now is the time for all good " +
    "men to come to the aid of their country.";
```

## 创建格式化字符串

使用`String`类的__类方法__`format()`方法，返回一个经过格式化的`String`对象。

举例：

```java
String fs;
fs = String.format("The value of the float " +
                   "variable is %f, while " +
                   "the value of the " + 
                   "integer variable is %d, " +
                   " and the string is %s",
                   floatVar, intVar, stringVar);
System.out.println(fs);
```
