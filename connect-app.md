# 概述

## 目标

实现远程调试一个启动的clojure应用。

## 在应用中内嵌一个 nREPL 服务器

创建一个测试项目:

```
lein new app testapp
cd testapp
```

在 testapp 项目的 project.clj 中添加 cider-nrepl 插件:

```
  :plugins [[cider/cider-nrepl "0.10.0"]]
```

编辑启动 clojure 文件:

```clojure
(ns testapp.core
 (:require [clojure.tools.nrepl.server :as nrepl-server]
           [cider.nrepl :refer (cider-nrepl-handler)]))

(defn my-add [a b]
  (+ a b))

(defn -main  [& args]
  (nrepl-server/start-server :port 7888 :handler cider-nrepl-handler)
  (println "I am in app!"))
```

然后 lein run 启动起来。

## 连接

Emacs 中使用Cider 来连接它。M+x cider-connect 然后输入 localhost, 端口 7888, 就连接上了， 可以在repl中尝试一下：

```clojure
user> (ns testapp.core)
nil
testapp.core> (my-add 1 1)
2
```


