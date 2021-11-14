# Spring事务

### 一.Spring事务管理器

#### 1.Spring事务管理结构

##### 1.Spring事务核心接口

![Spring事务核心接口](../../../image/框架/Spring/Spring事务核心接口.png)

### 3.Spring事务实现

#### 1.Spring编程式事务

##### 1.XML+Annotation（jdbcTemplate)

- 配置applicationContext.xml配置文件

![1.编程式事务(jdbcTemplate)配置xml文件](../../../image/框架/Spring/1.编程式事务(jdbcTemplate)配置xml文件.png)

- 编写Service层（具体事务）

![1.编程式事务(jdbcTemplate)编写service层](../../../image/框架/Spring/1.编程式事务(jdbcTemplate)编写service层.png)

- 测试事务

![1.编程式事务(jdbcTemplate)测试事务](../../../image/框架/Spring/1.编程式事务(jdbcTemplate)测试事务.png)

##### 2.XML+Annotation（TransactionTemplate)

- 配置applicationContext.xml配置文件

![2.编程式事务(TransactionTemplate)配置xml文件](../../../image/框架/Spring/2.编程式事务(TransactionTemplate)配置xml文件.png)

- 编写Service层（具体事务）

![2.编程式事务(TransactionTemplate)编写service层](../../../image/框架/Spring/2.编程式事务(TransactionTemplate)编写service层.png)

- 测试事务

![2.编程式事务(TransactionTemplate)测试事务](../../../image/框架/Spring/2.编程式事务(TransactionTemplate)测试事务.png)









