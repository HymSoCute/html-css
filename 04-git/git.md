## Git 介绍

Git 是一款开源免费的分布式的版本控制系统。是 Linux 之父 Linus Torvalds （**林纳斯·托瓦兹**）为了方便管理 Linux 内核代码而开发的。

## 作用

版本控制系统在项目开发中作用重大，能记录文件的历史状态，主要的功能有以下几点

- 代码备份
- 版本回退
- 协作开发
- 权限控制

### 下载安装

下载地址 <https://git-scm.com/>

## Linux 常用命令

Linux 是一套开源免费的操作系统。与系统的交互通常用命令来实现，常用的命令有：

- ==ls== 查看当前文件夹下的文件 （list 单词的缩写） `ls -al` 查看隐藏文件并竖向排布
- pwd 查看当前文件夹的路径 （Print Working Directory 缩写）
- ==cd== 进入某一个文件夹内 （change directory 缩写） ==cd ..== 回到上一级 ==Tab 键自动补全路径==
- clear 清屏（也可以使用 ==ctrl + l== 快捷键）
- mkdir 创建文件夹（make directory）
- touch test.html 创建一个文件
- rm test.html 删除文件 remove
- rm dir -r 删除文件夹 (-r 删除文件夹选项 -f 强制) force
- mv test.html t.html 移动文件，重命名 move 缩写
- cat test.html 查看文件内容
- ctrl + c 取消命令 (cancel)
- Tab 自动补齐路径
- 上下方向键，可以查看命令历史 (history 查看所有的历史命令)

Vim 是一款命令行下的文本编辑器，编辑方式跟图形化编辑器不同

- `vim test.html` 编辑文件（文件不存在则创建）
- i、a、 o、 进入编辑模式(i insert)
- `ESC` + `:wq` 保存并退出
- `ESC` + `:q!` 不保存并退出

![img](assets/vim-vi-workmodel.png)

## Git 使用

### 起始配置

第一次使用 Git 的时候，会要求我们配置用户名和邮箱，用于表示开发者的信息

```shell
git config --global user.name "Your Name"

git config --global user.email "email@example.com"
```

> ==注意命令之间的空格==

可以使用 `git config -l`命令来查看配置信息

### 基本操作

Git 的起始操作包括以下几个步骤

1. 创建进入空文件夹
2. 右键 -> 点击 Git Bash Here 启动命令行
3. `git init` 仓库初始化
4. 创建一个初始化文件 index.html
5. `git add index.html` 将文件加入到暂存区
6. `git commit -m '注释'` 提交到仓库 m 是 message 单词的缩写

![Git 步骤情况介绍](assets/Git 步骤情况介绍.jpg)

### .git 目录

![1576587724690](assets/1576587724690.png)

- hooks 目录包含客户端或服务端的钩子脚本，在特定操作下自动执行。
- info 包含一个全局性排除文件，可以配置文件忽略
- logs 保存日志信息
- objects <span style='color:red'>目录存储所有数据内容</span>,本地的版本库存放位置
- refs 目录存储指向数据的提交对象的指针（分支）
- config <span style='color:red'>文件包含项目特有的配置选项</span>
- description 用来显示对仓库的描述信息
- HEAD 文件指示目前被检出的分支
- index 暂存区数据

> 切记： <span style="color:red">不要手动去修改 .git 文件夹中的内容</span>

### 版本库的三个区域

- 工作区（代码编辑区）
- 暂存区（修改待提交区）
- 仓库区（代码保存区）

![img](https://ss1.bdstatic.com/70cFuXSh_Q1YnxGkpoWK1HF6hhy/it/u=2469289094,3249956923&fm=26&gp=0.jpg)

### 常用命令

- ==git status== 版本状态查看
- ==git add -A== 添加所有新文件到暂存区
- ==git commit -m '注释 '== 提交修改并注释
- `git commit -a -m '注释'` 一步提交（新增文件不会提交）
- `git diff` 查看工作区与暂存区的差异（不显示新增文件） 显示做了哪些修改
- `git diff --cached` 查看暂存区与仓库的差异
- `git restore --staged .` 将修改移除暂存区
- `git checkout -- .` 抹掉工作区的修改（不会删除新建的文件）

### 历史版本回滚

#### 回滚

查看历史记录

```shell
git log
git log --oneline
```

> 如果内容偏多， 需要使用方向键上下滚动， 按 `q` 退出

根据版本号进行回滚

```shell
git reset --hard  b815fd5a6ae655b521a31a9
```

> 进行版本回退时，不需要使用完整的哈希字符串，前七位即可
>
> 版本切换之前，要提交当前的代码状态到仓库

#### 找不到版本号的情况

查看所有的操作记录

```sh
git reflog
```

#### 其他回滚（了解）

```sh
git reset --hard HEAD^    回滚到上个版本
git reset --hard HEAD^^   回滚到上上个版本
```

### 配置忽略文件

##### 仓库中没有提交该文件

项目中有些文件是不需要进入版本库中，比如编辑器的配置。Git 中需要创建一个文件 ==.gitignore==，一般与 .gitignore 同级目录。

```sh
# 忽略所有的 .idea 文件夹
.idea
# 忽略所有以 .test 结尾的文件
*.test
# 忽略 node_modules 文件和文件夹
/node_modules
```

> .gitignore 可以在子文件夹下创建

##### 仓库中已经提交该文件

对于已经加入到版本库的文件，可以在版本库中删除该文件，然后再使用 `.gitignore` 配置忽略

```sh
git rm --cached .idea
```

然后在 .gitignore 中配置忽略

```sh
.idea
```

add 和 commit 提交即可

### 分支

分支是 Git 重要的功能特性之一，开发人员可以在主开发线的基础上分离出新的开发线。

#### 基本操作

##### 创建分支

name 为分支的名称

```sh
git branch name
```

查看分支

```sh
git branch
```

##### 切换分支

```sh
git checkout name
```

##### 合并分支

```sh
git merge name
```

##### 删除分支

```sh
git branch -d name
```

##### 切换并创建分支

```sh
git checkout -b name
```

> 注意: <span style="color:red">每次在切换分支前 提交一下当前分支</span>

#### 冲突

当多个分支修改同一个文件后，合并分支的时候就会产生冲突。冲突的解决非常简单，将内容修改为最终想要的结果，然后继续执行 git add 与 git commit 就可以了。

## GitHub

### 介绍

GitHub 是一个 Git 仓库管理网站。可以创建远程中心仓库，为多人合作开发提供便利。

### 使用流程

GitHub 远程仓库使用流程较为简单，主要有以下几种场景：

#### 本地有仓库

1. 注册并激活账号

2. 创建仓库

3. 获取仓库的地址

4. ==本地配置远程仓库的地址==

   ```shell
   git remote add origin https://github.com/xiaohigh/test2.git
   //远端仓库管理
   add  添加
   origin 远端仓库的别名
   https://github.com/xiaohigh/test2.git    仓库地址
   ```

5. 本地提交（确认代码已经提交到本地仓库）

6. 将本地仓库内容推送到远程仓库

   ```shell
   git push -u origin master
   //
   push 推送
   -u   关联, 加上以后,后续提交时可以直接使用 git push
   origin 远端仓库的别名
   master 本地仓库的分支
   ```

#### 本地没有仓库

1. 注册并激活账号

2. 克隆仓库

   ```shell
   git clone https://github.com/xiaohigh/test2.git
   ```

3. 增加和修改代码

4. 本地提交

   ```shell
   git add -A
   git commit -m 'message'
   ```

5. 推送到远程

   ```shell
   git push origin master
   ```

> 克隆代码之后， 本地仓库会默认有一个远程地址的配置， 名字为 origin

#### 多人合作

##### 账号仓库配置

GitHub 团队协作开发也比较容易管理，可以创建一个组织

- ==首页 -> 右上角 `+` 号-> new Organization==
- 免费计划
- 填写组织名称和联系方式（不用使用中文名称）
- 邀请其他开发者进入组织（会有邮件邀请）

组织创建完毕后，==在组织中创建仓库==

- 仓库创建完毕后 点击仓库的 settings 设置
- 左侧 Collaborators & teams
- 右侧 Teams 设置团队与权限 👌
- 如果没有 Team 需要先创建 Team（小组）

##### 协作流程

第一天

- 得到 Git 远程仓库的地址和账号密码

- 将代码克隆到本地（地址换成自己的）

  ```shell
  git clone https://github.com/xiaohigh/test.git
  ```

- 切换分支

  ```
  git checkout -b xiaohigh
  ```

- 开发代码

- 本地提交

  ```shell
  git add -A
  git commit -m '注释内容'
  ```

- 合并分支

  ```shell
  git checkout master
  git merge xiaohigh
  ```

- 更新本地代码

  ```shell
  git pull
  //或者使用下面两行代码
  git fetch
  git merge origin/master
  ```

- 提交代码

  ```shell
  git push
  ```

##### 工作流程

第二天流程

1. 更新代码
2. 切换分支
3. 开发功能
4. 提交
5. 合并分支
6. 提交本地代码
7. 更新代码
8. 提交代码

##### 冲突解决

同分支冲突一样的处理，将代码调整成最终的样式，提交代码即可。

##### <span style='color:blue'>免密登录</span>

1. 创建非对称加密对

   ```sh
   ssh-keygen -t rsa -C "xxx@xxx.com"
   ```

2. 文件默认存储在家目录（c:/用户/用户名/.ssh）的 .ssh 文件夹中。

   - id_rsa 私钥
   - id_rsa.pub 公钥

3. 将公钥（.pub）文件内容配置到账号的秘钥中

   ==首页 -> 右上角头像-> settings -> SSH and GPG keys -> new SSH Key==

4. 克隆代码时，选择 ssh 模式进行克隆 （地址 在仓库首页 绿色 克隆的位置 选择 use ssh）

   ```shell
   git clone git@github.com/xiaohigh/team-repo-1.git
   ```

### GitFlow

GitFlow 是团队开发的一种最佳实践，将代码划分为以下几个分支

![img](assets/o_git-workflow-release-cycle-4maintenance.png)

- Master 主分支。上面只保存正式发布的版本
- Hotfix 线上代码 Bug 修复分支。开发完后需要合并回 Master 和 Develop 分支，同时在 Master 上打一个 tag
- Feather 功能分支。当开发某个功能时，创建一个单独的分支，开发完毕后再合并到 dev 分支
- Release 分支。待发布分支，Release 分支基于 Develop 分支创建，在这个 Release 分支上测试，修改 Bug
- Develop 开发分支。开发者都在这个分支上提交代码

首次克隆完代码后，需要切换到开发分支

```sh
//查看所有分支
git branch -a
//切换分支
git checkout -b dev origin/dev
```

## 附录

### Git 官方书籍

[https://git-scm.com/book/zh/v2/%E8%B5%B7%E6%AD%A5-%E5%85%B3%E4%BA%8E%E7%89%88%E6%9C%AC%E6%8E%A7%E5%88%B6](https://git-scm.com/book/zh/v2/起步-关于版本控制)

### CRLF

CRLF 是 Carriage-Return Line-Feed 的缩写。

CR 表示的是 ASCII 码的第 13 个符号 \r 回车，LF 表示的是 ASCII 码表的第 10 个符号 \n 换行。

每个操作系统对回车换行的存储方式不同

- windows 下用 CRLF（\r\n）表示
- linux 和 unix 下用 LF（\n）表示
- mac 系统下用 CR（\r）表示

![打字机](assets/打字机.jpg)

### 远程仓库配置

本地仓库经常需要进行远程仓库的推送和更新，本地仓库可以配置远程仓库别名便于操作，常用命令有

查看使用方法

```shell
git remote -h
```

增加远程仓库

```shell
git remote add origin https://github.com/xiaohigh/learn.git
```

查看远程仓库配置

```
git remote -v
```

### 常见错误

#### 回车换行转换问题

```sh
warning: LF will be replaced by CRLF in 5.html.
The file will have its original line endings in your working directory
```

这个问题主要是 Git 在你提交时自动地把回车（CR）和换行（LF）转换成换行（LF），没有影响，==这里建议大家保留这个状态==。如果实在觉得警告难受，可以设置不转换

```sh
git config --global core.autocrlf false // 不推荐
```

### 提交报错

![img](assets/1532788288.bmp)

其他人已经提交过，本地代码需要更新，首先运行 git pull 命令

### 冲突提醒

![1574235172869](assets/1574235172869.png)

编辑冲突

### 提交错误

```sh
xiaohigh@DESKTOP-252ML8M MINGW64 /d/www/BJ0819/day13/代码/1-GitHub/7-test-ssh/8-https-to-ssh (master)
$ git push
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master
```

如果第一次将本地仓库分支提交到远程时，直接使用 `git push` 可能会报这个错误，解决方法

```sh
git push -u origin master
```

### 提交错误

```
 refusing to merge unrelated histories
```

解决方法

```
git pull origin master --allow-unrelated-histories
```

### 提交错误

![1576840150520](assets/1576840150520.png)

当前所在文件夹不是一个 git 仓库目录，切换目录工作

### 找不到 .git 的方法

![1582943996890](assets/1582943996890.png)
