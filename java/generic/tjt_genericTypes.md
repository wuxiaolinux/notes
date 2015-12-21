Generic Types
===

**泛型就是被参数化的类型。**下面通过一个例子来简单介绍下泛型。

## 普通的`Box`类

没有泛型的`Box`类型，代码是这样的：

```java
public class Box {

	private Object object;

	public void setObject(Object object) {
		this.object = object;
	}

	public Object getObject() {
		return object;
	}
}
```

`setObject()`方法可以接受任何对象，所以在编译期无法验证这个类是如何被使用的。

假如，这个对象原本是接受一个`Integer`对象，那么在调用`getObject()`方法的地方，正确的做法应该是将`getObject()`方法的返回值强制转换为`Integer`类型。

**然而，如果别人向`setObject()`方法错误地传递了一个`String`对象，那么强制转换就会出现错误。**

## 泛型版本的`Box`类

泛型类定义的格式：

`class name<T1, T2, ..., Tn> { /* ... */ }`

按此格式修改`Box`类型为泛型类：

```java
public class Box<T> {

	private T t;

	public void set(T t) {
		this.t = t;
	}

	public T get() {
		return t;
	}
}
```

> `T`可以是任何类、接口、数组类型或另一个类型变量，但不允许是基础类型。

## 类型参数命名惯例

**惯例有两点：**

* **单个字母**

* **大写形式**

最普遍使用的类型参数命名有：

* `E` - 代表元素，在集合框架里被大量使用

* `K` - Key

* `N` - Number

* `T` - Type

* `V` - Value

* `S`, `U`, `V` - 这几个也是常用的

## 调用和实例化泛型

#### 1. 改变声明引用变量的方式

声明普通的引用变量，如：

```java
Box box;
```

使用泛型后：

```java
Box<Integer> box;
```

> 你可以将泛型调用看做是普通的方法调用，但你传递的是类型参数（type argument）而不是一个普通参数。比如上面的例子，传递的类型参数就是`Integer`。

**关于术语parameter与argument的区别：**
<br/>
> **Type Parameter and Type Argument Terminology**: Many developers use the terms "type parameter" and "type argument" interchangeably, but these terms are not the same. When coding, one provides type arguments in order to create a parameterized type. Therefore, the `T` in `Foo<T>` is a type parameter and the `String` in `Foo<String> f` is a type argument.

**简单地说，parameter用在方法定义、类定义时，argument用在调用时。**

#### 2. 创建泛型对象

泛型调用叫做参数化类型，就是将一个类型参数化，所以这个过程要提供一个参数（类型参数）。

类型参数化且创建对象，像这样：

```java
Box<Integer> box = new Box<Integer>();
```

> 在 Java SE 7 以后，上面的例子可以改写为`Box<Integer> box = new Box<>();`

## 多类型参数

泛型可以具有多个类型参数，比如：

```java
public interface Pair<K, V> {
	public K getKey();
	public V getValue();
}
```

提供实现类`OrderedPair`：

```java
public class OrderedPair<K, V> implements Pair<K, V> {
	
	private K key;
	private V value;

	public OrderedPair(K key, V value) {
		this.key = key;
		this.value = value;
	}

	public K getKey() {
		return key;
	}

	public V getValue() {
		return value;
	}
}
```

创建两个`OrderedPair`实例：

```java
Pair<String, Integer> p1 = new OrderedPair<String, Integer>("Even", 8);
Pair<String, String>  p2 = new OrderedPair<String, String>("hello", "world");
```

实例化`p1`时，`K`是`String`，`V`是`Integer`。实例化`p2`时，`K`是`String`，`V`是`String`。

## 参数化类型

在实例化一个泛型时，可以使用另一个泛型作为这个泛型的一个类型参数，比如：

```java
OrderedPair<String, Box<Integer>> p = new OrderedPair<>("primes", new Box<Integer>());
```
