
## 为什么用sitemesh？

一般用include标签引进网站公共部分，比如top、bottom，如果每个页面都用include标签，显得非常冗余。为了解耦，使用sitemesh...

## 配置方法

### 相关jar

下载 & 引入jar，不多说。

### web.xml

在web.xml配置过滤器：

```xml
<filter>
  <filter-name>sitemesh</filter-name> 
  <filter-class>com.opensymphony.module.sitemesh.filter.PageFilter</filter-class> 
</filter> 
<filter-mapping> 
  <filter-name>sitemesh</filter-name> 
  <url-pattern>/*</url-pattern> 
</filter-mapping>
```

### decorators.xml

在WEB-INF目录下新建decorators.xml文件，内容结构类似：

```xml
<?xml version="1.0" encoding="utf-8" ?>   
<decorators defaultdir="/decorator">  
  <decorator name="main" page="main.jsp">  
    <pattern>/page/a.jsp</pattern>   
    <pattern>/page/b.jsp</pattern>  
  </decorator>  
  <decorator name="panel" page="panel.jsp"></decorator>  
</decorators> 
```
