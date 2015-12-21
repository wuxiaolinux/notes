Raw Types
===

原始类型（raw type）是泛型类或泛型接口不带任何类型参数的类型名称。

## Example

举个例子，假如有泛型类：

```java
public class Box<T> {
    public void set(T t) { /* ... */ }
    // ...
}
```

那么，创建一个参数化类型，需要给这个泛型提供一个类型参数，像这样：

```java
Box<Integer> intBox = new Box<>();
```

这里，类型参数是`Integer`，但如果不提供给参数`T`任何类型参数，那就是在创建这个泛型的原始类型：

```java
Box rawBox = new Box();
```

那么可以说：`Box`是泛型`Box<T>`的原始类型。

> **注意：非泛型类或接口不是原始类型！原始类型是相对于泛型来说的！**

## 兼容以往代码

原始类型出现在以往的代码中，因为很多 API 类在 JDK 5.0 之前都不是泛型的，实际上，泛型特性直到 JDK 5.0 才提供。

当使用原始类型时，实际上是无法展示泛型行为的，它就像一个普通的类。

另外，为了向后兼容，可以把一个参数化类型赋值给其泛型对应的原始类型，比如：

```java
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;
rawBox.set(8);  // warning: unchecked invocation to set(T)
```

可以使用`rawBox`调用泛型的`set(T)`方法，但不会有类型检查，实际上是在调用`set(Object)`方法，此时，`8`被自动装箱为`Integer`对象，进而转换为`Object`对象。如果用`stringbox`调用`set(T)`方法，就会由类型检查，实际上是在调用`set(String)`方法，任何给方法传递非`String`对象都将出现编译错误！

> 
> 总结一下
> 
> * 参数化类型与原始类型可以相互赋值
> 
> * 调用泛型方法时，注意引用变量的类型，如果引用变量是泛型，那么调用的时泛型方法，具有类型检查。如果引用变量是原始类型，那么就没有类型检查，泛型方法中的类型参数都是`Object`类型的。

## 编译器的Unchecked信息

原始类型与泛型混用一般会出现编译器警告，举个栗子：

```java
public class WarningDemo {
    public static void main(String[] args){
        Box<Integer> bi;
        bi = createBox();
    }

    static Box createBox(){
        return new Box();
    }
}
```

`unchecked`意味着编译器没有足够的信息进行必要的类型检查来确保类型安全，`unchecked`警告是关闭的，但是默认通过编译器给出一个提示信息。

查看详细`unchecked`警告，使用`-Xlint:unchecked`参数重新编译，比如：

```java
WarningDemo.java:4: warning: [unchecked] unchecked conversion
found   : Box
required: Box<java.lang.Integer>
        bi = createBox();
                      ^
1 warning
```

如果不想看到任何警告信息，有两种方式：

* 编译时，使用选项`-Xlint:-unchecked`

* 代码中使用注解`@SuppressWarnings("unchecked")`

<br/>
_-DONE-_
<br/><br/>

> <br/><br/>
> 推荐阅读
> 
> - [类型擦除](http://docs.oracle.com/javase/tutorial/java/generics/erasure.html)
> <br/><br/>

