# 开发环境搭建

## Leiningen

可以直接 brew install leiningen 。 也可以手动下载：

```shell
	# 下载 lein 脚本
	wget https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein
	# 设置执行权限
	chmod +x ./lein
	# 移动到 /usr/local/bin/ 中
	cp ./lein /usr/local/bin/
	# 运行下 lein， 第一次运行会自动下载必需的jar包
	lein
```

注意: 可能在最后执行 lein ，下载的时候遇到墙的问题。vpn 伺候一下。

## Emacs

直接下载一个 Emacs For Mac OS X : http://emacsformacosx.com

然后安装一个 el-get 插件, el-get 是一个第三方的emacs包管理器, 在 ~/.emacs 中添加脚本:

```lisp
;; el-get 
(add-to-list 'load-path "~/.emacs.d/el-get/el-get")
(unless (require 'el-get nil 'noerror)
  (with-current-buffer
      (url-retrieve-synchronously
       "https://raw.github.com/dimitri/el-get/master/el-get-install.el")
    (goto-char (point-max))
    (eval-print-last-sexp)))

;; 这个用来解决 emacs gui下 M+x cider-jack-in 会包找不到 lein 的问题
(defun set-exec-path-from-shell-PATH ()
  (let ((path-from-shell (shell-command-to-string "TERM=vt100 $SHELL -i -c 'echo $PATH'")))
    (setenv "PATH" path-from-shell)
    (setq exec-path (split-string path-from-shell path-separator))))

(when window-system (set-exec-path-from-shell-PATH))
```

然后运行下 Emacs, 第一次启动会自动安装 el-get。

## Cider

在 Emacs 中， M+x el-get-install cider 安装。

## cider-nrepl

在 ~/.lein/profiles.clj 中编辑，加入下边内容:

```clojure
	{:repl {:plugins [[cider/cider-nrepl "0.10.0"]]}}
```

## 测试

在 Emacs 中 M+x cider-jack-in 会打开一个 repl。

## 引用

- Leiningen: http://leiningen.org
- Emacs: http://www.gnuemacs.org
- Emacs For Mac OS X : http://emacsformacosx.com
- el-get: https://github.com/dimitri/el-get
- Cider: https://github.com/clojure-emacs/cider
- cider-nrepl: https://github.com/clojure-emacs/cider-nrepl
