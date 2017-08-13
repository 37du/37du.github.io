---
layout: post
title: tmux 常用命令
categories: tools, tmux
description:  tmux 常用命令
keywords: tmux, command, tools, efficient
---

| 命令 | 描述 |
| ------- |:-----------:|-----------------:|
| tmux new-session | 创建一个未命名的会话。可以简写为 tmux new 或者就一个简单的 tmux|
| tmux new -s development | 创建一个名为 development 的会话 |
| tmux new -s development -n editor | 创建一个名为 development 的会话并把该会话的第一个窗口命名为 editor |
| tmux attach -t development | 连接到一个名为 development 的会话 |
| PREFIX d | 从一个会话中分离，让该会话在后台运行. |
| PREFIX : |  进入命令模式 |
| PREFIX c | 在当前 tmux 会话创建一个新的窗口，是 new-window 命令的简写 |
| PREFIX 0...9 | 根据窗口的编号选择窗口 |
| PREFIX w | 显示当前会话中所有窗口的可选择列表 |
| PREFIX , | 显示一个提示符来重命名一个窗口 |
| PREFIX & | 杀死当前窗口，带有确认提示 |
| PREFIX % | 把当前窗口垂直地一分为二，分割后的两个面板各占 50% 大小 |
| PREFIX " | 把当前窗口水平地一分为二，分割后的两个面板各占 50% 大小 |
| PREFIX o | 在已打开的面板之间循环移动当前焦点 |
| PREFIX q | 短暂地显示每个面板的编号 |
| PREFIX x | 关闭当前面板，带有确认提示 |
| PREFIX SPACE | 循环地使用 tmux 的几个默认面板布局 |
| set -g prefix C-a | 设置前缀键为 CTRL-a |
| set -sg escape-time n |  设置 tmux 等待前缀键和命令键之间的时间间隔（毫秒） |
| source-file [file]  | 加载一个配置文件。重新加载当前配置文件或以后加入附加配置选项。 |
| bind C-a send-prefix | 两次按下 PREFIX 键后向 tmux 发送组合键 |
| bind-key [key] [command] | 新建一个快捷键，执行指定的 command。可简写为 bind |
| bind-key -r [key] [command]  | 新建一个可重复的快捷键，就是说只需按下一次 PREFIX 键之后就可以重复地按下命令键。当你想要在元素之间循环移动或调整面板大小时非常有用。可简写为 bind |
| unbind-key [key] | 移除一个定义的快捷键，让它绑定到其它命令。可简写为 unbind |
| display-message 或 display | 在状态消息里显示给定的文字 |
| set-option [flags] [option] [value] | 配置会话选项。使用 -g 选项可作为全局配置 |
| set-window-option [option] [value] | 配置窗口选项，例如活动通知，光标移动，或其它与窗口和面板相关的元素 |
| set -a | 把值添加到当前选项而不是替换选项的值 |
|tmux new-session -s development -n editor | 创建一个名为 development 的会话，将第一个窗口命名为 editor |
| tmux attach -t development | 连接到一个名为 development 的会话 |
| tmux send-keys -t development '[keys]' C-m | 向 development 会话的活动窗口或面板发送键盘命令，C-m 相当于按下回车键 |
| tmux send-keys -t development:1.0 '[keys]' C-m | 向 development 会话的第 1 个窗口和第 1 个面板发送键盘命令，C-m 相当于按下回车键 |
| tmux select-window -t development:1 | 选择 development 会话的第 1 个窗口，让它作为活动窗口 |
| tmux split-window -v -p 10 -t development |  在 development 会话里垂直地分割当前窗口，把它分为水平的 2 个面板并设置它的高度为总窗口大小的 10% |
| tmux select-layout -t development main-horizontal | 设置 development 会话的布局为 main-horizontal |
| tmux -f app.conf attach | 加载配置文件 app.conf 并连接到由这个配置文件所创建的一个会话 |
| tmuxinator open [name] | 在项目名 [name] 路径下使用默认的编辑器打开配置文件。如果不存在就创建一个新的配置文件 |
| tmuxinator [name] | 对指定项目加载 tmux 会话。如果会话不存在或无法连接到会话就根据项目的配置文件创建一个新会话 |
| tmuxinator list | 列出当前的项目 |
| tmuxinator copy [source] [destination] | 复制一个项目配置文件 |
| tmuxinator delete [name] | 删除指定的项目 |
| tmuxinator implode | 删除当前所有的项目 |
| tmuxinator doctor | 使用 tmuxinator 和系统配置查找问题 |
| PREFIX [ | 进入复制模式 |
| PREFIX ] | 粘贴当前缓存区的内容 |
| PREFIX = | 列出所有粘贴缓存区并粘贴选中的缓存内容 |
| CTRL -b | 向上翻滚一个屏幕的位置 |
| CTRL - f | 向下翻滚一个屏幕的位置 |
| g | 跳转到缓存区的顶部 |
| G | 跳转到缓存区的底部 |
| ? | 在缓存区内向后查找 |
| / | 在缓存区内向前查找 |
| show-buffer | 显示当前缓存区内容 |
| capture-pane | 捕捉指定面板的可视内容并复制到一个新的缓存区 |
| list-buffers | 列出所有的粘贴缓存区 |
| choose-buffer | 显示粘贴缓存区并粘贴选择的缓存区内的内容 |
| save-buffer [filename] | 保存缓存区的内容到指定文件里 |


在某个Session 内， 想再创建一个 独立的Session:
ctrl-a :new            To create a new session, then
ctrl-a s                  to interactively select and attach to the session.

