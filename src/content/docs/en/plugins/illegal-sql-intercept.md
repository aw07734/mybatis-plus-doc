---
title: Illegal SQL Interceptor Plugin
sidebar:
  order: 7
---

## Introduction

`IllegalSQLInnerInterceptor` is a security control plugin in the MyBatis-Plus framework, designed to intercept and inspect illegal SQL statements. This plugin helps developers identify and resolve potential security issues before SQL execution, such as full-table updates, delete operations, and index checks.

- Plugin Source 👉 [IllegalSQLInnerInterceptor](https://gitee.com/baomidou/mybatis-plus/blob/3.0/mybatis-plus-jsqlparser-support/mybatis-plus-jsqlparser/src/main/java/com/baomidou/mybatisplus/extension/plugins/inner/IllegalSQLInnerInterceptor.java)
- Test Cases 👉 [IllegalSQLInnerInterceptorTest](https://gitee.com/baomidou/mybatis-plus/blob/3.0/mybatis-plus-jsqlparser-support/mybatis-plus-jsqlparser/src/test/java/com/baomidou/mybatisplus/test/extension/plugins/inner/IllegalSQLInnerInterceptorTest.java)

## Features

- **Interception of SQL Types**: The plugin can identify and intercept specific types of SQL statements, such as high-risk operations like full-table updates or deletes.
- **Mandatory Index Usage**: Ensures the use of indexes in queries to improve performance and avoid full-table scans.
- **Full-Table Update/Delete Checks**: Prevents unauthorized full-table updates or deletes, reducing the risk of data loss.
- **`not`, `or`, and Subquery Checks**: Performs additional checks on SQL statements containing `not`, `or` keywords or subqueries to prevent logical errors or performance issues.

## Usage

**Java Configuration Example**

```java
@Configuration
public class MybatisPlusConfig {

    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        // Add the illegal SQL interceptor
        interceptor.addInnerInterceptor(new IllegalSQLInnerInterceptor());
        return interceptor;
    }
}
```

**XML Configuration Example**

```xml
<bean id="mybatisPlusInterceptor" class="com.baomidou.mybatisplus.extension.plugins.MybatisPlusInterceptor">
    <property name="interceptors">
        <list>
            <bean class="com.baomidou.mybatisplus.extension.plugins.inner.IllegalSQLInnerInterceptor"/>
        </list>
    </property>
</bean>
```

:::note

- **Review Official Documentation**: Before using the plugin, carefully read the official MyBatis-Plus documentation to understand detailed usage instructions and configuration methods.
- **Custom Adaptation**: This plugin provides a solution for intercepting illegal SQL, but it may not suit all enterprise environments. Developers should modify and optimize the plugin according to their project requirements.

:::

The `IllegalSQLInnerInterceptor` plugin is a powerful security tool provided by MyBatis-Plus, helping developers identify and resolve potential SQL security issues in advance. Proper configuration and use of this plugin can significantly enhance the security and efficiency of database operations.
