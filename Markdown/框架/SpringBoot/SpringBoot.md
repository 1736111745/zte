# SpringBoot

### 一.HelloWorld

#### 1.Maven方式创建HelloWorld

1. 创建普通maven项目-SpringBootMavenOne

2. 引入SpringBoot父工程依赖

   ```xml
   <parent>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-parent</artifactId>
       <version>2.3.4.RELEASE</version>
   </parent>
   ```

3. 引入SpringBoot-web场景启动器依赖

   ```xml
   <dependency>
       <groupId>org.springframework.boot</groupId>
       <artifactId>spring-boot-starter-web</artifactId>
   </dependency>
   ```

4. 写HelloWorld主程序类（启动类）

   ```java
   package com.ayl.boot;
   
   import org.springframework.boot.SpringApplication;
   import org.springframework.boot.autoconfigure.SpringBootApplication;
   
   /*
   1.标识当前类为SpringBoot的主类，是主程序类
   */
   @SpringBootApplication
   public class MainApplication {
       public static void main(String[] args) {
           SpringApplication.run(MainApplication.class,args);
       }
   }
   ```

5. 编写测试业务类

   ```java
   package com.ayl.boot.controller;
   
   import org.springframework.web.bind.annotation.RequestMapping;
   import org.springframework.web.bind.annotation.RestController;
   
   /*
   1.@RestController=@ResponseBody+@Controller
   2.@RequestMapping 表示当前方法为一个Handler处理器 请求地址为hello
   */
   @RestController
   public class HelloController {
   
       @RequestMapping("hello")
       public String HandlerOne(){
           return "Hello SpringBoot Two";
       }
   }
   ```

6. 发送请求

   ```http
   http://localhost:8080/hello
   ```

7. 返回结果

   ```text
   Hello SpringBoot Two
   ```

8. 补充

   > @ResponseBody
   > 1.在使用 @RequestMapping后，返回值通常解析为跳转路径
   > 2.但是加上 @ResponseBody 后返回结果不会被解析为跳转路径，而是直接写入 HTTP response body 中
   > 3.在使用此注解之后不会再走视图处理器，而是直接将数据写入到输入流中，等同于通过response对象输出指定格式的数据（解析对象为json格式的字符串）
   >
   >
   > @Controller
   > 1.@Controller用于标记在一个类上，使用它标记的类就是一个SpringMvc Controller对象
   > 2.分发处理器(DispatcherServlet 会扫描使用该注解的类的方法，并检测该方法是否使用了@RequestMapping注解
   > 3.@Controller只是定义了一个控制器类，而使用@RequestMapping注解的方法才是处理请求的处理器

   

#### 3.简单的修改服务器默认端口

1. 使用 `SpringBootMavenOne项目` 代码
2. 在resources文件夹下创建文件-































