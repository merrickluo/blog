+++
title = "开始使用 Spacemacs"
date = "2015-12-12T01:14:46+08:00"
slug = "start-use-spacemacs"
+++

## 开始使用 Spacemacs
虽说上一篇 Blog 已经是在很久之前，但是上篇刚说了不爱用 vim 的快捷键，现在就开始用 spacemacs 貌似有些奇怪=。=

我为什么开始使用 vim 的 keybinding 呢，说来话长，一切都要从坑爹的 Xcode 说起...（省略对 Xcode 的 1w 字吐槽）总之因为 Xcode 无法支持 Emacs 的 keybinding（别说 Karabiner，这玩意儿影响太多东西），然后自带的 keybinding 效率实在太低，于是我不得不开始使用 XVim，然后在背叛 Emacs 的道路上越走越远（强力推荐 Chrome 的插件 cVim）。

但是我不得不说，spacemacs 确实相当的好用，之前也有试过 oh-my-emacs 等等配置，然后自己也乱七八糟配过一些，都谈不上好用，而且还有一些相当麻烦的问题，虽说 spacemacs 问题也不不少，好在最后都找到了解决方案，下面就来记录一下配置时遇到的一些小问题。

## 安装spacemacs
参见[官方文档](https://github.com/syl20bnr/spacemacs)，就不再赘述

装好之后，打开Emacs，

    find-file ~/.spacemacs

## Emacs behind proxy
要想正常使用软件，第一件事就是配好代理，Emacs 里面的包管理，shell，都是需要代理的，所以第一步就是要配好代理

在dotspacemacs/user-init() 中

    (setq url-proxy-services
        '(("no_proxy" . "^\\(localhost\\|10.*\\)")
          ("http" . "proxy_host:port")
          ("https" . "proxy_host:port")))

C-x，C-e and you are good to go.
这里需要一个 http 的代理，如果用 shadowsocks 转一下就好。

## Fonts
字体不对简直不想写代码，所以先配好字体

英文字体

    (setq-default dotspacemacs-default-font '("Essential PragmataPro"
                                            :size 14
                                            :weight normal
                                            :width normal
                                            :powerline-scale 1.1))

中文字体

    (dolist (charset '(kana han symbol cjk-misc bopomofo))
    (set-fontset-font (frame-parameter nil 'font)
                      charset (font-spec :family "Source Han Sans SC"
                                         :size 13)))
  

## Fish in Emacs

接下来是比较麻烦的部分，至于为什么要在 Emacs 中用 Fish，没办法，Emacs 党就是喜欢 one to rule them all。

首先安装 spacemacs 提供的 shell layer 并配置一下默认 shell

    (shell :variables
            shell-default-term-shell "/usr/local/bin/fish"
            shell-default-height 30
            shell-default-position 'bottom)

然后打开 ansi-term，你会发现几个问题：

a) prompt 下面会多出一个回车符号，在 dotspacemacs/user-init() 里加入

      (add-hook 'term-mode-hook
            (lambda ()
              (toggle-truncate-lines)
              (make-local-variable 'transient-mark-mode)
              (setq transient-mark-mode nil)))

b) prompt title 显示问题

    find-file ~/.config/fish/config.fish

加上

    function fish_title
        true
    end

c) fish 的自动提示出现时，会显示一个 4m 并换行，同样在 dotspacemacs/user-init() 中

    (setq system-uses-terminfo nil)

暂且到另一个 terminal 中，如果 emacs 是用 Homebrew 安装的，执行以下命令

    tic -o ~/.terminfo /usr/local/share/emacs/24.5/etc/e/eterm-color.ti
    
其他安装方法，请自行找到类似目录

## kotlin-mode
目前 kotlin 官方并没有支持Emacs，只在github上搜到了两个repo，[这个]()以及[这个]()，目前没有发现有什么区别。

参照 spacemacs 自定义 layer 的方法并使用以上两个中任意一个即可获得 kotlin 代码的语法高亮显示。

## magit
magit 的安装非常简单，安装 spacemacs 自带的 git layer 即可，唯一的问题是文档中提到的默认将 magit-status 的 buffer 打开全屏的设置方法失效了，经过一番查询后，现在需要一个第三方的 extesion 才能实现。

这个在.spacemacs 中搜索一下加在对应位置即可

    (setq dotspacemacs-additional-packages'(fullframe))

dotspacemacs/user-config() 中

    (fullframe magit-status magit-mode-quit-window)

重新同步 packages 即可。

## TODO

1. 补充链接

## History
2015.12.12 initial version
2015.12.13 kotlin-mode 和 magit


