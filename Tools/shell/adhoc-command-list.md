# 工具命令列表

本文记录实现特定功能的简短命令行

## 文件

### 将当前目录下文件内容中的所有foo替换为bar

使用`find`找文件,使用`sed`替换
`find . -type f -exec sed -i 's/foo/bar/g' {} +`

### 将当前目录下文件名中的foo替换为bar

使用`rename`
`rename -v -- 's/foo/bar/' *`

### 通过xargs对特定文件执行操作

以`rm`为例:
`... | xargs -I {} rm {}`

## 进程

### 批量结束包含某关键字的进程

使用`cut`
`ps -ef|grep LOCAL=NO|grep -v grep|cut -c 9-15|xargs kill -9`
>`cut -c 9-15` 是截取输入行的第9个字符到第15个字符，而这正好是进程号PID

使用`awk`
`ps x|grep gas|grep -v grep |awk '{print $1}'|xargs kill -9`

## 磁盘

### 查看磁盘各分区大小

使用人类易读的单位
`df -h`

使用`1k`为单位
`df`

### 查看foo目录大小

只看该目录
`du -sh foo`

递归查看子目录
`du -h foo`

> 加`-a`查看隐藏文件


### 卸载设备

1. 查看设备位置
`df -h`

2. 根据设备的`path`卸载  
`umount path`
        
        
### 检查已经被删掉的临时数据
`lsof | grep delete`

## 网络

### 查看网卡速率

`mii-tool`

> eth0: negotiated 100baseTx-FD, link ok 100M

上面的结果就是网卡速率100M的意思

