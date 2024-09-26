# 后端问题与解决

## 1.跨域问题

**两种解决跨域问题的方法有什么区别，该如何选用？目前未知....**

这是之前用来解决跨域问题的config类

```
/*
* 打通前后端，解决前后端跨域问题
* */
@Configuration
public class CorsConfig implements WebMvcConfigurer {

    /*
    * 允许服务器接收任意收到的"GET", "HEAD", "POST", "PUT", "DELETE", "OPTIONS"请求
    * 不限制请求头格式
    * */
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

本次项目学习到的解决跨域问题的config类

```
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.cors.CorsConfiguration;
import org.springframework.web.cors.reactive.CorsWebFilter;
import org.springframework.web.cors.reactive.UrlBasedCorsConfigurationSource;

@Configuration
public class GulimallCorsConfiguration {

    @Bean
    public CorsWebFilter corsWebFilter(){
        UrlBasedCorsConfigurationSource urlBasedCorsConfigurationSource = new UrlBasedCorsConfigurationSource();

        CorsConfiguration corsConfiguration = new CorsConfiguration();
        //配置跨域
        corsConfiguration.addAllowedHeader("*");
        corsConfiguration.addAllowedMethod("*");
//        corsConfiguration.addAllowedOrigin("*");spring boot 2.4版本以下才使用这个
        corsConfiguration.addAllowedOriginPattern("*");
        corsConfiguration.setAllowCredentials(true);

        urlBasedCorsConfigurationSource.registerCorsConfiguration("/**",corsConfiguration);
        return new CorsWebFilter(urlBasedCorsConfigurationSource);
    }
}
```



## 2.mp的basemapper与Iservice

关于mp中的basemapper与IService之间的关系：

public class BrandServiceImpl extends ServiceImpl<BrandDao, BrandEntity> implements BrandService
你看继承ServiceImpl的时候就在泛型传了一个BrandDao，这样brandServiceimpl也就继承了basemapper
<font color='orange'>todo :这里到底是怎么实现的，关于泛型，以后可以深入了解一下!!!!!</font>



**总之，这里可以直接使用更便捷的this.basemapper.xxx，而不需要使用this(也就是brandserviceimpl)的update**

<img src="C:\Users\赵联城\AppData\Roaming\Typora\typora-user-images\image-20240925130501598.png" alt="image-20240925130501598" style="zoom: 67%;" />













# 前端问题与解决





## 1.@Change

在使用elementUI组件中的表格中的自定义动态表单时，我使用了一个按钮，结果@click怎么点击都不触发，最后发现得使用@change

对前端的很多东西都不熟悉啊！！！尤其是和vue相关的y

```
      <el-table-column prop="showStatus" header-align="center" align="center" label="显示状态">
        <template slot-scope="scope">
          <el-switch v-model="scope.row.showStatus" active-color="#13ce66" inactive-color="#ff4949"
            @change="updateShowStatus(scope.row)">
          </el-switch>
        </template>
      </el-table-column>
```



## 2. 滑块默认值问题

**<font color='orange'>如代码所示，如果你没有使用v-bind，那么你设置的serachType初始值是无法生效的</font>**

<font color='red'>**reason:因为你没有使用v-bind,vue会认为滑块的1和0是字符串，而你设置的serachType是数字，不用v-bind那就都统一使用字符串，想统一使用数字就得v-bind;实际上v-bind很智能，会根据你设置的serachType的类型来自动匹配**</font>

```
      dataForm: {
        attrId: 0,
        attrName: '',
        searchType: 1,
        icon: '',
        valueSelect: '',
        attrType: '',
        enable: '',
        catelogId: '',
        showDesc: ''
      },
```



```
      <el-form-item label="是否需要检索" prop="searchType">
        <el-switch v-model="dataForm.searchType" active-color="green" inactive-color="red" active-value='1'
          inactive-value='0' @change="test(dataForm.searchType)">
        </el-switch>
      </el-form-item>
```



## 3.el-cascader标签的坑

**<font color='red'>el-cascader 标签中的 v-model必须接受的是一个数组！！！不然报错</font>**

```
      <el-form-item label="所属分类" prop="catelogIds">
        <el-cascader :options="menus" v-model="dataForm.catelogIds" :props="props">
        </el-cascader>
      </el-form-item>
```

既然聊到这个标签，顺便简单介绍一下:props="props"，用来匹配配置，options是指向数据

```
      props: {
        value: 'catId',
        label: 'name',
        children: 'children'
      },
```







































# 后端收获

## 1.JSR303

常规简单数据校验可以使用JSR303, 剩余的复杂数据校验再由你自己来写











# 前段收获



## 1.OSS单图片上传

<font color='orange'>**①父组件:注意这个dataForm.logo,就是父组件传给子组件的**</font>

```
      <el-form-item label="品牌logo地址" prop="logo">
        <!-- <el-input v-model="dataForm.logo" placeholder="品牌logo地址"></el-input> -->
         <FileUpload v-model="dataForm.logo"></FileUpload>  
      </el-form-item>
```





<font color='orange'>**②解析子组件**</font>

需要注意的知识：

- elementUI的这些属性如果是方法则不需要给参数，底层会自动给，为了让使用者专注业务逻辑
- this.value的值是在handleUploadSuccess方法中赋予的,最初父组件传的数据是空，后面文件上传成功后才赋值给this.value
  当this.value有值的时候，才会填充到fileList,然后就实现了数据回显。（不理解就看代码，easy）
- 在 Vue 框架中，**触发 `input` 事件可以更新父组件的值**，这是因为 `v-model` 的工作机制就是基于子组件内部触发 `input` 事件来实现的。通过这个事件传递数据，父组件能够接收到子组件的最新值，并且更新它的 `v-model` 绑定的属性。
- this.$emit("input", this.fileList[0].url); this.$emit，触发自定义事件input,你可能好奇明明也没定义自定义input事件啊，其实
  像input,blur（失去焦点），change,click,keyup等等，这是约定成俗的自定义事件，无需创建即可使用。
- 使用占位符 `${filename}` 而不是直接使用 `file.name` 主要是为了增强安全性、灵活性、避免文件覆盖，以及符合对象存储服务的签名策略和路径控制要求。这种方法确保每个上传的文件都有唯一的路径，并且可以与服务端上传策略结合，确保安全性和文件管理的方便性。//当然不是强制要求占位符，你直接用file.name也可以，当你对文件名进行处理，如加上时间戳、UUID）确保上传的文件名在存储系统中是唯一的，比如我们这里就用UUID处理过了，可以直接file.name

```vue
<template>
  <div>
  	//elementUI相关组件，有问题查文档
    <el-upload
      class="upload-demo"
      action="https://gulimall-zlc123.oss-cn-hangzhou.aliyuncs.com"
      multiple
      list-type="picture"
      :file-list="fileList"
      :data="dataObj"
      :before-upload="beforeUpload" 
      :on-success="handleUploadSuccess"
      :show-file-list="showFileList">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="fileList[0].url" alt="">
    </el-dialog>
  </div>
</template>

<script>
import { v4 as uuidv4 } from 'uuid';

export default {
   //这个value就是父组件传的属性,后面有大用
  props: {
    value: String
  },
  computed: {
      //下面三个计算属性,关于file
    imageUrl() {
      return this.value;
    },
    imageName() {
      if (this.value != null && this.value !== '') {
        return this.value.substr(this.value.lastIndexOf("/") + 1);
      } else {
        return null;
      }
    },
    fileList() {
      return [{
        name: this.imageName,
        url: this.imageUrl
      }]
    },
      //控制图片回显，没传图片就不显示，传了就显示；注意计算属性要修改就得提供set方法,而且得是:{},而非(){}
    showFileList: {
      get() {
        return this.value !== null && this.value !== '' && this.value !== undefined;
      },
      set(newValue) {}
    }
  },
  data() {
    return {
      dialogVisible: false,
      dataObj: {
        policy: '',
        signature: '',
        key: '',
        ossaccessKeyId: '',
        dir: '',
        host: ''
      },
    };
  },
  methods: {
    // 文件上传前处理
    beforeUpload(file) {
        //必须要使用promise，否则可能出现还没有收到后端的签名，文件就已经上传了，没有签名违反规则会导致400错误
      return new Promise((resolve, reject) => {
        this.$http({
          url: this.$http.adornUrl('/thirdparty/oss/policy'),
          method: 'get',
        }).then(({ data }) => {
          console.log("接收数据:", data);
          this.dataObj.policy = data.policy;
          this.dataObj.host = data.host;
          this.dataObj.signature = data.signature;
          //"${filename}" 阿里云对象存储的上传策略中的预处理，就是一个占位符，等文件上传成功后再回过头来赋值
          //可是明明可以直接file.name不就完事了？
          this.dataObj.key = data.dir + uuidv4() + "${filename}";
          this.dataObj.ossaccessKeyId = data.ossAccessKeyId;
          this.dataObj.dir = data.dir;
          resolve(); // 确保上传可以继续
        }).catch(error => {
          console.error("请求签名失败:", error);
          reject(); // 阻止上传
        });
      });
    },
    // 文件上传成功后
    handleUploadSuccess(res, file) {
      console.log("上传成功后的file", file);
      this.showFileList = true;
      //父组件开始给的值是空，会给fileList添加一个空的file，得先将其干掉
      this.fileList.pop();
      this.fileList.push({ name: file.name, url: this.dataObj.host + '/' + this.dataObj.key.replace("${filename}", file.name) });
        //数据回显给父组件
      this.$emit("input", this.fileList[0].url);
    }
  },
}
</script>

```















# 收货与感想



1. <font color='orange'>**学习到了 逆向工程的使用，这些代码生成器可以极大地提高项目构建速度**</font>
2. maven版本依赖问题，配置地狱，各种莫名其妙的Bug，无法解决的恶性bug，接踵而来。
3. 很重要的一点是，我使用到了elementUi的使用，对一些基础组件的调用有了认识，之前都没有怎么用过
4. 





















# 待完成功能



## 1.拖拽功能



## 2. 自定义jsr303































# 待解决问题



## 1.多图片上传

**<font color='red'>明明想做成多图片上传，但每次上传多个就有问题</font>**

```
<template>
  <div>
    <el-upload class="upload-demo" action="https://gulimall-zlc123.oss-cn-hangzhou.aliyuncs.com" :multiple="true"
      :list-type="listType" :file-list="fileList" :data="dataObj" :before-upload="beforeUpload"
      :on-success="handleUploadSuccess" :show-file-list="showFileList">
      <el-button size="small" type="primary">点击上传</el-button>
      <div slot="tip" class="el-upload__tip">只能上传 jpg/png 文件，且不超过 500kb</div>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <li v-for="file in this.fileList">
        <img width="100%" :src="file.url" alt="图片" />
      </li>
    </el-dialog>
  </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
  props: {
    value: {
      type: [Array, String], // 支持 Array 和 String
      default: () => [], // 默认值为空数组
    },
    listType: {
      type: String,
      default: "picture-card",
    },
  },
  computed: {
    fileList() {
      console.log("filelist被修改了")
      let fileList = [];
      for (let i = 0; i < this.value.length; i++) {
        fileList.push({ url: this.value[i] });
      }
      console.log("初始化的filelist",fileList)
      return fileList;
    },
    showFileList: {
      get() {
        return this.fileList.length > 0; // 判断是否有文件
      },
      set(newValue) {
        // 可选：这里你可以处理新的值
      },
    },
  },
  data() {
    return {
      dialogVisible: false,
      dataObj: {
        policy: "",
        signature: "",
        key: "",
        ossaccessKeyId: "",
        dir: "",
        host: "",
      },
    };
  },
  methods: {
    emitInput(fileList) {
      let value = [];
      for (let i = 0; i < fileList.length; i++) {
        value.push(fileList[i].url);
      }
      this.$emit("input", value);
    },
    beforeUpload(file) {
      console.log("文件上传前的 file", file);
      return new Promise((resolve, reject) => {
        this.$http({
          url: this.$http.adornUrl("/thirdparty/oss/policy"),
          method: "get",
        })
          .then(({ data }) => {
            console.log("接收数据:", data);
            this.dataObj.policy = data.policy;
            this.dataObj.host = data.host;
            this.dataObj.signature = data.signature;
            this.dataObj.key = data.dir + uuidv4() + file.name;
            this.dataObj.ossaccessKeyId = data.ossAccessKeyId;
            this.dataObj.dir = data.dir;
            resolve(); // 确保上传可以继续
          })
          .catch((error) => {
            console.error("请求签名失败:", error);
            reject(); // 阻止上传
          });
      });
    },
    handleUploadSuccess(res, file) {
      console.log("上传成功后的 file", file);
      this.fileList.push({
        name: file.name,
        url: this.dataObj.host + "/" + this.dataObj.key,
      });
      console.log("上传成功后的fileList", this.fileList)
      // 数据回显
      this.emitInput(this.fileList);
      console.log("数据回显后的fileList", this.fileList)
    },
  },
};
</script>

```



## 2.OrderId





### 3.学习init

学习init方法,  和  dataForom提交时，一个方法解决save与update的思路

















































































































