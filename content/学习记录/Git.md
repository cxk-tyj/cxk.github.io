# 一.安装[Git - 下载 - Git 版本控制系统](https://git-scm.cn/downloads)

## 二.配置
配置用户名 
`git config --global user.name "your.name"`
 配置用户邮箱 
`git config --global user.email "email@wxample.com"`

## 三.创建本地仓库
在任意一个路径下新建一个文件夹——>cd file——>打开git bash执行
`git init`%%初始化仓库%%

## 四.工作流程
![[git本地工作流.png]]
## 五.常用指令
### 1.工作区->暂存区
%% git add 单个文件/目录/通配符 %%
`git add .`

### 2.暂存区->本地仓库
`git commit -m '注释内容'`

### 3.日志查看
`git log [option]`
%%option很多，可指定长命令为别名%%

### 4.版本回退
`git reset --hard commitID`
%%commitID可使用git log查看%%

查看已经删除的记录
`git reflog`

### 5.指定不需要git控制的文件
创建`.gitignore`文件%%文件名固定%%。
使用编辑器打开该文件，添加不需要控制的文件名或者使用正则表达式。

