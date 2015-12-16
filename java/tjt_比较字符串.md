Comparing Strings and Portions of Strings
===

字符串间的比较，比较字符串的一部分，方法包括：

* `boolean endsWith(String suffix)`

    如果字符串以参数指定的字符串结束，返回true，反之false。

* `boolean startsWith(String prefix)`

    如果字符串以参数指定的字符串开始，返回true，反之false。

* `boolean startsWith(String prefix, int offset)`

    假设把字符串从索引offset开始截取形成一个新字符串，如果这个字符串以参数指定的字符串开始，返回true，反之false。

* `int compareTo(String anotherString)`

    比较this和参数字符串，依据字典顺序。如果this大于参数字符串，返回正整数，如果相等，返回0，如果小于，返回负整数。

* `int compareToIgnoreCase(String str)`

    和上面那个方法唯一的不同就是忽略大小写差异。

* `boolean equals(Object anObject)`

    仅仅当anObject是字符串对象，并且字符序列与this字符序列一致时，返回true。

* `boolean equalsIgnoreCase(String anotherString)`

    比较两个字符串的字符序列是否一致，忽略大小写。

* `boolean regionMatches(int toffset, String other, int ooffset, int len)`

    this字符串的一部分与参数字符串的一部分的字符序列是否相同，区分大小写。this字符串索引位置区间`[toffset, toffset + len - 1]`与参数字符串索引位置区间`[ooffset, ooffset + len - 1]`上的字符序列是否相同。

* `boolean regionMatches(boolean ignoreCase, int toffset, String other, int ooffset, int len)`

    与前一个方法一样的作用，但不区分大小写。

* `boolean matches(String regex)`

    this字符串是否匹配指定正则表达式

### 举例：搜索字符串

代码：

```java
public class RegionMatchesDemo {
    public static void main(String[] args) {
        String searchMe = "Green Eggs and Ham"; // 原字符串
        String findMe = "Eggs"; // 目标字符串
        int searchMeLength = searchMe.length(); // 原字符串长度
        int findMeLength = findMe.length(); // 目标字符串长度
        boolean foundIt = false; // 搜索结果

        // 从原字符串索引位置(searchMeLength - findMeLength)开始，到字符串结束，刚好是目标字符串的长度。
        // 没必要再将索引位置后移！
        for (int i = 0; i <= (searchMeLength - findMeLength);  i++) {
           if (searchMe.regionMatches(i, findMe, 0, findMeLength)) {
              foundIt = true;
              System.out.println(searchMe.substring(i, i + findMeLength));
              break;
           }
        }
        if (!foundIt) {
            System.out.println("No match found.");
        }
    }
}
```

代码原文解释：

> The program steps through the string referred to by searchMe one character at a time. For each character, the program calls the regionMatches method to determine whether the substring beginning with the current character matches the string the program is looking for.