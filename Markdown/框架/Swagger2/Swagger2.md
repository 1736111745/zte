# Swagger2

### 一.SpringBoot集成Swagger2

#### 1.启动Swagger2

##### 1.导入依赖

```xml

<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger2 -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
    <version>2.9.2</version>
</dependency>

<!-- https://mvnrepository.com/artifact/io.springfox/springfox-swagger-ui -->
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
    <version>2.9.2</version>
</dependency>
```

##### 2.启动Swagger2

```java
@Configuration//标识当前类为配置类
@EnableSwagger2//启动Swagger2
public class SwaggerConfig {
    @Bean //Docket是Swagger唯一的Bean实例，Swagger的配置信息全部通过Docket对象来进行配置
    public Docket docket() {
        return new Docket(DocumentationType.SWAGGER_2);
    }
}
```

![Swagger2基础配置](../../image/框架/Swagger/Swagger2/Swagger2基础配置.png)

##### 3.测试访问Swagger2

```http
http://localhost:8080/swagger-ui.html
```

##### 4.显示效果

![Swagger2基础显示效果](../../image/框架/Swagger/Swagger2/Swagger2基础显示效果.png)

#### 2.配置Swagger2文档信息

##### 1.Docket对象部分源码解析

```java
public class Docket implements DocumentationPlugin {
  ...
  private ApiInfo apiInfo = ApiInfo.DEFAULT;//
  private String groupName = DEFAULT_GROUP_NAME;
  private boolean enabled = true;
  private GenericTypeNamingStrategy genericsNamingStrategy = new DefaultGenericTypeNamingStrategy();
  private boolean applyDefaultResponseMessages = true;
  private String host = "";
  private Optional<String> pathMapping = Optional.absent();
  private ApiSelector apiSelector = ApiSelector.DEFAULT;
  private boolean enableUrlTemplating = false;
  private List<VendorExtension> vendorExtensions = newArrayList();
  ...
}
```

##### 2.ApiInfo对象部分源码解析

```java
public class ApiInfo {
  public static final Contact DEFAULT_CONTACT = new Contact("姓名", "url", "邮箱");//作者默认信息
  public static final ApiInfo DEFAULT = new ApiInfo("这里会有默认值");//默认ApiInfo的值
  private final String version; //版本号
  private final String title;//标题
  private final String description;//描述
  private final String termsOfServiceUrl;//组织url
  private final String license;//开源版本号
  private final String licenseUrl;//开源版本号url
  private final Contact contact;//作者信息
  private final List<VendorExtension> vendorExtensions;//供应商扩展
}
```

##### 3.配置文档信息

```java
@Configuration//标识当前类为配置类
@EnableSwagger2//启动Swagger2
public class SwaggerConfig {
    @Bean //配置docket以配置Swagger具体参数
    public Docket docket() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo());
    }

    //配置文档信息
    private ApiInfo apiInfo() {
        Contact contact = new Contact("安宜龙", "https://gitee.com/an-yilong", "aylone@sina.com");
        return new ApiInfo(
                "安宜龙的Swagger2API文档", // 标题
                "这是SpringBoot项目的API文档", // 描述
                "v1.0", // 版本
                "https://gitee.com/an-yilong", // 组织链接
                contact, // 联系人信息
                "Apach 2.0 许可", // 许可
                "许可链接", // 许可连接
                new ArrayList<>()// 扩展
        );
    }
}
```

##### 4.显示效果解析

![image-20211109223016421](../../image/框架/Swagger/Swagger2/Swagger2显示效果解析.png)

#### 3.配置Swagger2扫描接口

- Swaager2通过调用 RequestHandlerSelectors对象的不同方法 从而实现不同的接口扫描方式

##### 1.扫描全部的包

```java
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()                             //select()Api扫描构建器
            .apis(RequestHandlerSelectors.any())  //any()方法,扫描全部的包
            .build();
}
```

##### 2.不扫描任何包

```java
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()                             //select()Api扫描构建器
            .apis(RequestHandlerSelectors.none())  //none()方法,不扫描任何包
            .build();
}
```

##### 3.扫描指定的包

```java
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()                             //select()Api扫描构建器
            .apis(RequestHandlerSelectors.basePackage("要扫描的包"))  //basePackage()方法,扫描指定的包
            .build();
}
```

##### 4.扫描指定的类注解

```java
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()   //withClassAnnotation()方法，参数为类注解的Class对象，使用该注解的类都会被扫描到           
            .apis(RequestHandlerSelectors.withClassAnnotation(RestController.class))
            .build();
}
```

##### 5.扫描指定的方法注解

```java
@Bean
public Docket docket() {
    return new Docket(DocumentationType.SWAGGER_2)
            .apiInfo(apiInfo())
            .select()   //withMethodAnnotation()方法，参数为方法注解的Class对象，使用该注解的方法都会被扫描到
            .apis(RequestHandlerSelectors.withMethodAnnotation(GetMapping.class))
            .build();
}
```

#### 4.配置Swagger2过滤路径

- 只扫描指定路径中的接口









































