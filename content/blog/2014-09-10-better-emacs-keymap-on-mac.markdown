+++
title = "在Mac上更好的使用Emacs快捷键"
date = 2014-09-10T01:08:11+08:00
slug = "better-emacs-keymap-on-mac"
+++

&nbsp; &nbsp; 不太记得自己为啥学了Emacs，大概是最开始听说作为程序员Emacs和Vim至少得会用一个，然后觉得Vim各种要按Esc傻傻的，所以就安心学习了Emacs的快捷键。不过要说作为一个Android开发者（虽说你强行要在Emacs中开发也不是不行，但是代价太大，我反正是放弃了），还是得用到IDE，不过好在的是，各种好用的IDE都是支持修改快捷键的，而且也早有大神们做好了各种Emacs的Keymap供我们使用（吐槽：不论是Eclipse还是Intellij自带的Emacs布局都不好用）。

&nbsp; &nbsp; 现在回到标题，其实Mac（OS X whatever）对Emacs爱好者可谓又爱又狠，爱的是，大部分编辑文本的地方都能用基本的Emacs光标移动等快捷键，恨的是这个可恶的Option按钮，他完全没办法作为Meta键使用，让我每次都按ESC？你等等，我先去跳个楼。不过好在的是Emacs爱好者们都遇到了这个问题，于是就有了解决方案。

&nbsp; &nbsp; 大部分的解决方案都是使用Ukulele这个软件重新编辑键盘布局，大致操作就是新建一个键盘布局，然后按住Option键，把所有键值都清掉，保存并放在~/Library/KeyboardLayout/中，最后到语言和输入法中选择这个键盘布局就搞定啦。还有一点要提一下的是，大部分的中文输入法都支持选择键盘布局，所以以后也可以保持在中文输入法状态下搬砖啦。
&nbsp; &nbsp; 
&nbsp; &nbsp; 另外上面的手动方法可能比较麻烦，大致介绍以下原理，这个[网站](http://wordherd.com/keyboards/)可以直接下载改好的键盘布局文件，直接放进去就能用了。

&nbsp; &nbsp;最后祝大家敲键盘愉快，小指头健康~
