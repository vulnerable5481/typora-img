# 1. IO流







# 2. 反射











# 3.Calandar







# 4.java时间类







# 5.Stream流详解

# 6.Lambda表达式 

# 7. Comparator











# 8.Comparator字符串切割







# 9.字符串操作





```
        //1.使用,分割descripts后，将其变成字符串封装
        spuInfoDescEntity.setDecript(String.join(",",decripts));
        
        //2.split
        String s = "xxx"
        String result = s.split("_")[0] 
```





# 10.枚举类



```
package com.zlc.common.constant;

public class WareConstant {
    public enum PurchaseStatusEnum{
        CREATED(0,"新建"),
        ASSIGNED(1,"已分配"),
        RECEIVED(2,"已领取"),
        FINISHED(3,"已完成"),
        HASERROR(4,"有异常");

        private int code;
        private String message;

        PurchaseStatusEnum(int code, String message) {
            this.code = code;
            this.message = message;
        }

        public int getCode() {
            return code;
        }

        public String getMessage() {
            return message;
        }
    }
}

```













































































































































































































