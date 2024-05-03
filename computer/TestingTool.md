## Swagger

### 导言

why:写完接口文档，你得去测试一下接口是否正确吧，传统方式使用Postman，但是postman传参不方便，参数一多效率就低，所以推荐一个更高效的测试工具 Swagge

what:使用Swagger你只需要按照它的规范去定义接口和接口相关的信息，就可以做到生成接口文档，以及在线接口调试页面

官网:https://swagger.io/



### 操作教程

`Knife4j`:是为Java MVC框架集成Swagger生成Api文档的增强解决方案

```
//knife4j  maven坐标
<dependency>
    <groupId>com.github.xiaoymin</groupId>
    <artifactId>knife4j-spring-boot-starter</artifactId>
</dependency>
```

1. 导入knife4j的maven坐标
2. 在配置类中加入knife4j相关配置
3. 设置静态资源映射，否则接口文档页面无法访问
   //**下面的代码需要的时候就自己复制粘贴，只需要修改里面的一些数据即可**

```
/**
 * 配置类，注册web层相关组件
 */
@Configuration
@Slf4j
public class WebMvcConfiguration extends WebMvcConfigurationSupport {
    /**
     * 通过knife4j生成接口文档
     * @return
     */
    @Bean
    public Docket docket() {
        ApiInfo apiInfo = new ApiInfoBuilder()
                .title("苍穹外卖项目接口文档")
                .version("2.0")
                .description("苍穹外卖项目接口文档")
                .build();
        Docket docket = new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo)
                .select()
                //指定生成接口需要扫描的包
                .apis(RequestHandlerSelectors.basePackage("com.sky.controller"))
                .paths(PathSelectors.any())
                .build();
        return docket;
    }

    /**
     * 设置静态资源映射
     * @param registry
     */
    protected void addResourceHandlers(ResourceHandlerRegistry registry) {
        registry.addResourceHandler("/doc.html").addResourceLocations("classpath:/META-INF/resources/");
        registry.addResourceHandler("/webjars/**").addResourceLocations("classpath:/META-INF/resources/webjars/");
    }
}
```

进行完以上三个步骤就可以 使用url进入swagger提供的一个页面 比如localhost:8080/doc.html，该页面就是swagger主页面

![image-20240110125041505](C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240110125041505.png)







### 常用注解

//通过注解可以控制生成的接口文档，是接口文档拥有更好的可读性

| **@Api**              |     **用在类上，例如Controller，标识对类的说明**     |      |
| --------------------- | :--------------------------------------------------: | ---- |
| **@ApiModel**         |           **用在类上，例如entity,dto,vo**            |      |
| **@ApiModelProperty** |             **用在属性上，描述属性信息**             |      |
| **@ApiOperation**     | **用在方法上，例如Controller的方法，说明方法的用途** |      |



### 注意事项









### 技巧



1. 可以配置全局变量来避免重复登录之类的,比如设置一个jwl令牌，就不需要登录

















































































