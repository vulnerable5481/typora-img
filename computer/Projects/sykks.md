# 一.感悟





# 二.问题杂谈





## 1.前后端跨域问题

1.1前端设置axios统一访问路径

![image-20240618212228809](https://zlc-typora.oss-cn-hangzhou.aliyuncs.com/img1/image-20240618212228809.png)

1.2 前端vue.config.js中设置代理

```
module.exports = {
    devServer: {
        host: 'localhost',
        open: true, // 自动打开浏览器
        // 代理配置表，在这里可以配置特定的请求代理到对应的API接口
        // 例如将'localhost:8080/api/xxx'代理到'www.example.com/api/xxx'
        proxy: {
            '/api': { // 匹配所有以 '/api'开头的请求路径
                target: 'http://localhost:8080', // 代理目标的基础路径
                // secure: false,  // 如果是https接口，需要配置这个参数
                changeOrigin: true, // 支持跨域
                pathRewrite: { // 重写路径: 去掉路径中开头的'/api'
                    '^/api': ''
                }
            }
        }
    }
}
```

2.1后端

```
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * 解决跨域问题
 */
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    @Override
    public void addCorsMappings(CorsRegistry registry) {
        registry.addMapping("/**")
                .allowedOriginPatterns("*")
                .allowedMethods("GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS")
                .allowCredentials(true)
                .maxAge(3600)
                .allowedHeaders("*");

    }
}
```





# 三.前端问题







# 四.后端问题





# 五.功能实现总结



## 1.单点登录





## 2.注册







## 3.当前连续签到天数

### ①思路

```
1.利用reids中 bitmap(图表) 二进制形式存储 签到天数
2.
```









# 六.待实现功能



## 1.websocket实现实施弹幕和聊天室,统计在线人数

























































































































































