---
tags: ['NeedWork']
---

# Vim


## Tips

### 强制使用sudo保存

**命令**

```bash
:w !sudo tee %
```

**解析**

* `w`  保存，此处为另存为，将当前文本内容作为下一个命令的标准输入
* `!`  代表之后的为外部命令
* `sudo tee` 命令行命令，以管理员权限将标准输入执行重定向到文件
* `%` 会扩展成为当前文件名

整个命令的意义就是，以当前文本内容覆盖当前文件，所以完成后会需要重新载入




## 参考
- https://www.ibm.com/developerworks/cn/linux/l-cn-tip-vim/
- http://blog.sina.com.cn/s/blog_5ac88b350100an4p.html

---