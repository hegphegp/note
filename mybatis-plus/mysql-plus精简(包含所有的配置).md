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

#### MybatisPlusConfig.java
```java
import com.baomidou.mybatisplus.MybatisMapWrapperFactory;
import com.baomidou.mybatisplus.mapper.ISqlInjector;
import com.baomidou.mybatisplus.mapper.LogicSqlInjector;
import com.baomidou.mybatisplus.spring.boot.starter.ConfigurationCustomizer;
import org.apache.ibatis.type.JdbcType;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import com.baomidou.mybatisplus.plugins.PaginationInterceptor;
/**可以定义注入多个ISqlInjector, ConfigurationCustomizer对象*/
@Configuration
public class MybatisPlusConfig {
    /** 如果是H2，postgresql，oracle数据库，还需要定义ID主键自增的生成器
    @Bean
    public IKeyGenerator keyGenerator(){
        return new H2KeyGenerator();
    }
     */
    /** mybatis-plus分页插件<br> */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }

    /**注入sql注入器,逻辑删除的SQL注入器*/
    @Bean
    public ISqlInjector sqlInjector(){
        return new LogicSqlInjector();
    }

    @Bean
    public ConfigurationCustomizer jdbcTypeForNullConfiguration(){
        return ((configuration)->
            configuration.setJdbcTypeForNull(JdbcType.NULL)
        );
    }

    @Bean
    public ConfigurationCustomizer MybatisMapWrapperFactoryConfiguration(){
        return ((configuration)->
                configuration.setObjectWrapperFactory(new MybatisMapWrapperFactory())
        );
    }

//    @Bean
//    public ConfigurationCustomizer MybatisMapWrapperFactoryConfiguration(){
//        return new ConfigurationCustomizer(){
//            @Value("${mybatis.return-map-to-camel-case:false}")
//            private Boolean mybatisMapWrapperFactory;
//
//            @Override
//            public void customize(org.apache.ibatis.session.Configuration configuration) {
//                if (mybatisMapWrapperFactory) {
//                    configuration.setObjectWrapperFactory(new MybatisMapWrapperFactory());
//                }
//            }
//        };
//    }
}
```
