# spring-data-jpa-mybatis
集成spring-data-jpa和mybatis

```java
public interface UserRepository extends JpaRepository<User, Integer> {
    // 只有该方法会由mybatis执行，其余方法按照jpa方式正常处理
    @MybatisQuery
    User selectByAccount(String account);
}
```

## 快速开始
参见单元测试
1. 添加依赖
    ```xml
    <dependency>
        <groupId>com.mario6</groupId>
        <artifactId>spring-data-jpa-mybatis</artifactId>
        <version>1.0.0-SNAPSHOT</version>
    </dependency>
    ```

2. 配置application.properties
    ```properties
    spring.datasource.url=jdbc:h2:mem:spring-data-jpa-mybatis?DB_CLOSE_ON_EXIT=TRUE
    spring.jpa.show-sql=true
    spring.jpa.format-sql=true
    # mybatis
    mybatis.type-aliases-package=com.mario6.springdata.jpa.mybatis.repository.demo.domain
    mybatis.mapper-locations=classpath*:mapper/*.xml
    mybatis.configuration.map-underscore-to-camel-case=true
    ```
3. 启动类添加注解
    ```java
    @SpringBootApplication
    @EnableMybatisJpaRepositories
    public class MybatisJpaApplication {}
    ```
    
4. 相关方法
    ```java
    public interface UserRepository extends JpaRepository<User, Integer> {
        @MybatisQuery
        User selectByAccount(String account);
    }
    ```
    
## 说明
你可以按照正常使用spring-data-jpa使用, 只有`@MybatisQuery`注解的方法才会由mybatis处理, 完全同mybatis一样, @Param注解使用也需要是mybatis的。