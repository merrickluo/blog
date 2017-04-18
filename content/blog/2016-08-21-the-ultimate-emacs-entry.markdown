+++
title = "The Ultimate Emacs Entry Point"
date = "2016-08-21T01:08:11+08:00"
slug = "the-ultimate-emacs-entry"
+++

最近对于工具有点疯魔（写不出代码只好折腾下工具了

## At first

Emacs作为一个Lisp Machine，启动时间虽说比其他操作系统快得多，但是由于经常会无意间被关机，导致大家对其启动速度印象深刻。
虽说 `emacs --daemon` 可以部分解决这个问题，但还是无法拯救喜欢乱按 space-q-q 的我（spacemacs用户），在这样的情况下呢，启动慢已经不是最让我烦心的事了，由于 `emacs --daemon`, 所以大部分的东西我都会用`emacscliet -c`来当作编辑器，如果daemon不小心被我自己干掉了，那么这些操作全部会中断。又得手动`emacs --daemon`，总之一个字，烦！

## So

于是就有了这么一个脚本

``` bash
#!/bin/sh
# making fcitx working in emacs
client="emacsclient"
# I dont want to start a new frame if there is one
frame_count=`emacsclient -e '(true-frame-count)' 2>/dev/null || echo -1`
# start server if not started 
if [ $frame_count -lt 0 ]; then
    LC_CTYPE=zh_CN.UTF-8 emacs --daemon
    client="$client -c"
    # make frame if no param coming
elif [ $frame_count -lt 1 ]; then
    client="$client -c"
fi
$client $@ 2>/dev/null
```
and in emacs init script:

```
(defun true-frame-count()
  (length
   (remove-if
    (lambda(f) (string-equal (terminal-name f) "initial_terminal"))
    (frame-list))))
```
因为如果以 --daemon 模式启动，就会有这样一个叫做 initial_terminal的frame强行说自己visible。

and in i3 config:

```ini
# emacs
focus_on_window_activation focus
```
## TODO

大概会看看用Automator怎么在OSX哦不，是macOS上实现类似的功能。（改名字真好玩，反正改名字的人不用搜索）。
