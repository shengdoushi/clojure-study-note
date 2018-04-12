# 概述

## 目标

在一个lein项目中添加maven的java库

## 示例

Alipay 的支付Java库: https://mvnrepository.com/artifact/com.alipay.sdk/alipay-sdk-java


## 添加 

在 project.clj 中添加到 :dependencies 下:

```clojure
  :dependencies [...
                 [com.alipay.sdk/alipay-sdk-java "3.0.0"]
				 ...]

```

## maven 的配置和 Leiningen 的配置转换

maven 的配置:

```
<!-- https://mvnrepository.com/artifact/com.alipay.sdk/alipay-sdk-java -->
<dependency>
    <groupId>com.alipay.sdk</groupId>
    <artifactId>alipay-sdk-java</artifactId>
    <version>3.0.0</version>
</dependency>
```

对应的 Leiningen 中 :dependencies 的配置:

```
;; https://mvnrepository.com/artifact/com.alipay.sdk/alipay-sdk-java
[com.alipay.sdk/alipay-sdk-java "3.0.0"]
```
