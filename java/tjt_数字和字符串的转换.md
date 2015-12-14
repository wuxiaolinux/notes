Converting Between Numbers and Strings
===

## 字符串转换为数字

每个基础数值类型的包装类都提供了一个类方法`valueOf()`，这个方法支持将字符串转换为其包装类的对象。

```java
public class ValueOfDemo {
    public static void main(String[] args) {

        // this program requires two 
        // arguments on the command line 
        if (args.length == 2) {
            // convert strings to numbers
            float a = (Float.valueOf(args[0])).floatValue(); 
            float b = (Float.valueOf(args[1])).floatValue();

            // do some arithmetic
            System.out.println("a + b = " +
                               (a + b));
            System.out.println("a - b = " +
                               (a - b));
            System.out.println("a * b = " +
                               (a * b));
            System.out.println("a / b = " +
                               (a / b));
            System.out.println("a % b = " +
                               (a % b));
        } else {
            System.out.println("This program " +
                "requires two command-line arguments.");
        }
    }
}
```

运行程序，使用`4.5`和`87.2`作为两个参数，输出：

```java
a + b = 91.7
a - b = -82.7
a * b = 392.4
a / b = 0.0516055
a % b = 4.5
```

注意：每个包装类还提供了类方法`parseXXX`，它的返回类型是基础类型，而不是对象。

## 数值转化为字符串

给出3种方式：

1. `+`操作符

2. `String`类的类方法`valueOf()`

3. 包装类的`toString()`类方法

分别给出示例代码：

```java
int i;
// Concatenate "i" with an empty string; conversion is handled for you.
String s1 = "" + i;

// The valueOf class method.
String s2 = String.valueOf(i);

int i;
double d;
String s3 = Integer.toString(i); 
String s4 = Double.toString(d); 
```

这有段代码，将数值转化为字符串，分别计算它小数点前后的数字的个数：

```java
public class ToStringDemo {
    
    public static void main(String[] args) {
        double d = 858.48;
        String s = Double.toString(d);
        
        int dot = s.indexOf('.');
        
        System.out.println(dot + " digits " +
            "before decimal point.");
        System.out.println( (s.length() - dot - 1) +
            " digits after decimal point.");
    }
}
```

运行，输出：

```java
3 digits before decimal point.
2 digits after decimal point.
```
