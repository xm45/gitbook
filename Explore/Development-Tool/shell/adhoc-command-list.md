# 工具命令列表

本文记录实现特定功能的简短命令行



## 批量结束包含某关键字的进程
* `ps -ef|grep LOCAL=NO|grep -v grep|cut -c 9-15|xargs kill -9`
* `ps x|grep gas|grep -v grep |awk '{print $1}'|xargs kill -9`