[新手必看](https://blog.csdn.net/Hanani_Jia/article/details/77950594)

[Git教程](https://www.liaoxuefeng.com/wiki/896043488029600)

[Git常见操作和常见错误](https://blog.csdn.net/f2006116/article/details/50779011)

# GitHub操作步骤
## 1.注册GitHub账号
- 打开 https://github.com ，注册（Signup）新帐号；
- 在设定的邮箱接收激活邮件，点击激活链接，激活新帐号。
## 2.Fork实验库
- 打开 https://github.com/17727263376/ApplicationGroupDaily
- 点击右上角的 Fork 按钮，将项目复制到个人帐号下：
## 3.安装Git工具
- 打开 https://git-scm.org ，下载适合本机版本（32位或64位）；
- 双击 exe 文件将工具安装到本机上；
- 从开始菜单打开Git-Shell。
## 4.克隆代码到本地磁盘
- 用 cd 命令切换到保存代码的路径上，如切换到D盘：
> $ cd d: 
- 用 clone 命令将个人库的代码克隆到本地磁盘：
> $ git clone (需要克隆的github网址)
- 进入本地项目源代码目录：
> $ cd ApplicationGroupDaily
## 5.编写笔记
- 下载有道云笔记编写笔记
- 右键另存为笔记至本地克隆地址
## 6.提交代码
```
git add . //add .意为添加所有文件，如需只添加一部分文件需输入文件名
git commit -m "year-month-day"
git push
```
## 7.发送合并请求
- 打开个人项目库
- 点击 New pull request 按钮；
- 检查自己所修改的文件是否正确。如果不正确，则按照之前的步骤重新修改；如果正确，则点击『Create pull request』绿色按钮。
## 8.最后一步
- Pull request发送之后，一定要自己查看自己修改过的文件，看看有没有改错文件（Files changed）。