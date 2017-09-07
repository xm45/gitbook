# 工具命令列表

本文记录实现特定功能的简短命令行


## 将当前目录下文件内容中的所有foo替换为bar
使用`find`找文件,使用`sed`替换
`find . -type f -exec sed -i 's/foo/bar/g' {} +`

## 将当前目录下文件名中的foo替换为bar
使用`rename`
` rename -v -- 's/foo/bar/' *`

## 批量结束包含某关键字的进程

使用`cut`
`ps -ef|grep LOCAL=NO|grep -v grep|cut -c 9-15|xargs kill -9`

使用`awk`
`ps x|grep gas|grep -v grep |awk '{print $1}'|xargs kill -9`