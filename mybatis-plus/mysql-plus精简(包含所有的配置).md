# 所有的配置精简版(不含任何的解释)

#### application.yml
```
mybatis-plus:
  global-config:
    #刷新mapper 调试神器
    refresh-mapper: true
    #逻辑删除配置(要配置3个参数,logic-delete-value,logic-not-delete-value,sql-injector,其中推荐sql-injector用@Bean进行注入)
    logic-delete-value: 0
    logic-not-delete-value: 1
  configuration:
    map-underscore-to-camel-case: true
    cache-enabled: false
```

#### 