Characters
===

`Character`类包含一个单一的字段，类型是`char`，`Character`提供一系列操作字符的类方法。

## 构造器

```java
Character ch = new Character('a');
```

## 自动装箱、拆箱

略……

## 类方法

```java
boolean isLetter(char ch)
boolean isDigit(char ch)
boolean isWhitespace(char ch)
boolean isUpperCase(char ch)
boolean isLowerCase(char ch)
char toUpperCase(char ch)
char toLowerCase(char ch)
toString(char ch)
```

## 转义字符

- `\t`	Insert a tab in the text at this point.

- `\b`	Insert a backspace in the text at this point.

- `\n`	Insert a newline in the text at this point.

- `\r`	Insert a carriage return in the text at this point.

- `\f`	Insert a formfeed in the text at this point.

- `\'`	Insert a single quote character in the text at this point.

- `\"`	Insert a double quote character in the text at this point.

- `\\`	Insert a backslash character in the text at this point.

举个例子，要输出`She said "Hello!" to me.`，则：

```java
System.out.println("She said \"Hello!\" to me.");
```



