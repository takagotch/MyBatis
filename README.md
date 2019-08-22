### myBatis
---
http://www.mybatis.org/mybatis-3/

```java
// src/main/java/org/apache/ibatis/session/defaults/DefaultSqlSessionFactory.java

public class DefaultSqlSessionFactory implements SqlSessionFactory {
  
  private final Configuration configuration;
  
  public DefaultSqlSessionFactory(Configuration configuration) {
    this.configuration = configuration;
  }
  
  @Override
  public SqlSession openSession() {
    return openSessionFromDataSource(configuration.getDefaultExecutorType(), null, false);
  }
  
  @Override
  public SqlSession openSession(boolean autoCommit) {
  
  }
  
}
```

```
```

```
```


