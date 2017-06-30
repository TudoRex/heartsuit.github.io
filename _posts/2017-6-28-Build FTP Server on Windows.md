---
layout: post
title: Win7 建立FTP站点（附CMD访问命令）
tags: Syetem
---
### Why am I doing this?!
> 由于公司内部网络限制，导致无法访问云端存储（云盘、云笔记等😢），但是自己安全感比较弱（安全意识较强😎），总希望所有文件能够定时备份；经过查询，发现有软件可以实现本地到FTP的传输，因此便折腾一番，将自己的笔记本作为FTP Server。目前软件正常运行，可实现定期备份（设置各种模式）。

### Win7 建立FTP站点
1. 安装IIS组件：
控制面板中打开程序和功能->点击打开或关闭windows功能->Internet 信息服务勾选->FTP服务器->->FTP服务，FTP扩展性->Web管理工具->IIS管理控制台->确定。
2. 建立FTP站点：
右键网站->选择添加FTP站点->FTP站点名称->物理路径->IP地址、端口号（FTP默认21）->自动启动FTP站点，SSL选择允许->下一步->身份验证：基本->授权：所有用户->权限：读取、写入（这个看自己需求）->完成。
3. 创建登录用户：
我的电脑->右键->管理->本地用户和组->用户->“右键”新建用户->输入用户名和密码->取消勾选“用户下次登录时须更改密码”->勾选密码永不过期->创建，此时新建的用户在Users组。
4. 检测FTP站点所选择物理路径的权限
物理路径 右键->属性->安全->在“组或用户名”下查看有无Users->如果没有，则点击编辑->添加->在“输入对象名称来选择”下输入Users->检查名称->确定->确定。
另外，可以对Users组设置读取、修改权限。
如果没有这一步，而物理路径的权限不对，则可能出现以下错误：
``` text
530-User cannot log in, home directory inaccessible.
Win32 error:Access is denied.Error details: File system denied the access.
530 End
```
5. 在浏览器或资源管理器中输入：`ftp://IP:Port`，输入创建的那个用户名、密码进行登录。
6. Done.

**Note**: Win10搭建FTP站点与此基本类似，需要注意的是Win10家庭版没有部分功能，eg：本地用户和组等，如果是家庭版，需要升级专业版才可以，`Win10家庭版升级专业版`，只需要更新即可，网上教程很多。

### CMD下使用FTP
打开cmd->ftp IP:Port->用户名、密码->登录成功

**一些常用命令：**

- ls or dir //资源列表；
- get FileName //下载文件，默认目录：C:\Users\Windows用户名\；
- put FileName //上传文件；
- mdelete FileName //删除文件；y确认；
- rename oldName newName //重命名（适用于文件、文件名）；
- mkdir DirectoryName //创建目录；
- rmdir DirectoryName //删除目录；
- bye or quit //退出；

---
***If you have any questions or any bugs are found, please feel free to contact me.***

***Your comments and suggestions are welcome!***