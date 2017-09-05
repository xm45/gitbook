---
tags: ["命令手册","FAQ"]
---
# FAQ

针对ubuntu使用时在命令行出现的种种问题的解决方案汇总

## tail: 无法使用 inotify 机制，回归为 polling 机制
临时解决问题（关机之后又是原来的设置）：
`sudo sysctl -w fs.inotify.max_user_watches=100000`

长期修改 inotify 文件监听上限：
`echo fs.inotify.max_user_watches=100000 | sudo tee -a /etc/sysctl.conf`

重载配置文件，使之马上生效
`sudo sysctl -p`

**来源**
[Error：达到了 inotify 观察数限制](http://www.markjour.com/article/cannot-add-inotify-watch.html)
