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
    return openSessionFromDataSource(configuration.getDefaultExecutorType(), null, autoCommit);
  }
  
  @Override
  public SqlSession openSession(TransactionIsolationLevel level) {
    return openSessionFromDataSource(configuration.getDefaultExecutorType(), level, false);
  }
  
  
  @Override
  public Configration getConfiguration() {
    return configuration;
  }
  
  private SqlSession openSessionFromDataSource(ExecutorType execType, TransactionIsolationLevel, boolean autoCommit) {
    Trasaction tx = null;
    try {
      final Environment environment = configuration.getEnvironment();
      final TransactionFactory transactionFactory = getTransactionFactoryFromEnvironment(environment);
      tx = transactionFactory.newTransaction(environment.getDataSource(), level, autoCommit);
      final Executor executor = configuration.newExecutor(tx, execType);
      return new DefaultSqlSession(configuration, executor, autoCommit);
    } catch (Exception e) {
      closeTransaction(tx);
      throw ExceptionFactory.wrapException("Error opening session. Cause: " + e, e");
    } finally {
      ErrorContext.instance().reset();
    }
  }
  
  private TransactionFacotry getTransactionFactoryFromEnvironment(Environment environment) {
    if (environment == null || environment.getTransactionFacotry() == null) {
      return new ManagedTransactionFactory();
    }
    return environment.getTransactionFactory();
  }
  
  private void closeTransaction(Transaction tx) {
    if (tx != null) 
      try{
        tx.close();
      } catch (SQLException ignore) {
        //
      }
  }
}
```

```
```

```
```


