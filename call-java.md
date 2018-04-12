# 概述

## 目标

在 clojure 代码中调用java

## 导入要用的java类

java 中:

```java
import java.text.SimpleDateFormat;
```

clojure:

```clojure
(import & import-symbols-or-lists)
;; import-symbols-or-lists 每项为 (package className*)

(import
 '(java.text SimpleDateFormat)
 '(org.apache.hadoop.hbase.client HTable Scan Scanner)
 '(org.apache.hadoop.hbase.filter RegExpRowFilter StopRowFilter))
```

## 创建对象

有两种方式， 一种是用 new 方法，一种是用 className. 方式：

```clojure
; new 方式
(new className args*)

(new SimpleDateFormat)
(new SimpleDateFormat "yyyy-mm-dd")

; className. 方式
(className. args*)

(SimpleDateFormat.)
(SimpleDateFormat. "yyyy-mm-dd")
```

## 调用静态方法

有两种方式, 一种是 / 方式，一种是用 . 方式:

```clojure
; /
(Classname/staticMethod args*)

(Long/parseLong "1231")

; .
(. Classname staticMethod args*)
(. Classname (staticMethod args*))

(. Long parseLong "1231")
(. Long (parseLong "1231"))

```

## 调用对象方法

用两种 . 方式，

```clojure

;
(. instance-expr method-symbol args*)
(. instance-expr (method-symbol args*))

(def rnd (java.util.Random. ))
(. rnd nextInt 10)
(. rnd (nextInt 10))

;
(. instance-expr method-symbol args*)

(.nextInt rnt 10)
```

## 获取类的静态变量，对象的成员变量

```clojure
(. Classname-symbol member-symbol)
(. instance-expr member-symbol)
(Classname-symbol/member-symbol)
(.fileld object)
(set! (.field object) val)

(. Calendar DECEMBER)
```

## .. 宏


```clojure
(. (. (Calendar/getInstance) (getTimeZone)) (getDisplayName))
```

的语法糖:

```clojure
(.. (Calendar/getInstance) (getTimeZone) (getDisplayName))
```

## doto 宏

```clojure
(doto instance
  method*)

(doto instance
  (method args*)*)
```

## memfn 宏

```clojure
(map #(.getBytes %) ["amit" "rob" "kyle"])
```

的语法糖

```clojure
(map (memfn getBytes) ["amit" "rob" "kyle"])
```

## bean 宏

用于转换一个对象为打印的clojure对象

```clojure
(bean (Calendar/getInstance))
```

