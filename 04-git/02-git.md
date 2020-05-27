# 笔记

## 今日大纲
* 复习
* VSCode
* Markdown
* GitHub 介绍与注册
* 本地仓库推送到远程仓库
* 仓库克隆
* GitHub 多人开发配置（组织创建）
* 免密登录（SSH）
* GitFlow 介绍
* GitHub 网页功能
* 码云
* GitLab
* Sourcetree

## vscode 安装 markdown 插件
Markdown All in One

## 临时邮箱
十分钟邮箱

## 1password 收费的
lastPass 免费的密码管理工具


## git remote add
就是添加远程仓库的别名

## 复盘
1. 创建 GitHub 仓库
   1. 点击 GitHub 首页右上角 + 第一个菜单
   2. 在表单页填写仓库的相关信息， 比如仓库名称，介绍，选择公有
   3. 不要勾选初始化 readme

2. 本地仓库创建
   1. 本地仓库做至少一次的提交
   2. 参照仓库首页的提示添加远程仓库别名
   3. 将本地仓库推送到远端 git push -u origin master

## 远程仓库的名字不要使用中文
但是Git仓库工作区的文件名称随意

## 仓库推送前、分支切换前、回滚历史前，都需要对本地的修改做一次提交

## git remote 
git remote 用来管理远程仓库的
* git remote -v 用来查看所有的别名以及对应的 URL 地址
* git remote add 用来添加远程仓库的别名
* git remote remove 删除
* git remote rename 更名

## git push
用来将本地仓库的分支推送到远程仓库
```
git push origin master
```
* origin 远程仓库的别名， 这里可以直接设置远程仓库的 URL
* master 为本地的分支名称

git push origin master:master


### 设置分支关联
* git push --set-upstream 
* git push -u
以上两个功能是一致的， 设置完毕之后就可以直接使用 git push 进行推送

## 克隆完仓库之后，一定要切换命令行的位置
* 克隆的仓库默认就有一个叫 origin 的远程配置

## git pull 用来拉取远程仓库的数据

## GitHub 网站上也可以对文件进行修改和删除， 但是不推荐


## -h 或者 --help 来查看命令的帮助

## 组长创建一个组织， 将组里的成员添加进来

## git 清理缓存的账号和密码
```
git credential-manager uninstall
```

## 组织成员只能对组织里的仓库有团队开发的权限
1. 创建组织仓库


## 关于协作开发
1. 远程仓库不一定是 GitHub 的地址
2. 克隆仓库 git clone http://github.com/xiaohigh/test.git dirname
3. 切换分支  cart
4. 开发项目
5. add commit 分支提交
6. 切换到主分支 git checkout master
7. 分支合并  git merge cart
8. 先做更新 git pull
9. 再做推送 git push origin master

## 对于空文件夹，Git 是不会记录和保存的
通过在文件夹下创建名为 .gitkeep 的文件来实现记录和跟踪

## 练习
1. 组长创建一个组织的仓库
2. 成员进行仓库克隆， 创建一个属于自己的文件 文件名格式 eg：荣浩.html
3. 将本地的代码进行提交，推送到远程仓库中。

## pull 与 clone
* git pull 只会拉取当前分支的内容
* git clone 是会拉取所有的内容

## 免密提交
1. 生成密钥对
2. 将公钥内容存放到 GitHub
3. 需要对远程仓库的 URL 进行调整.
   1. 克隆使用 ssh 形式的 url
   2. 对于已经存在的仓库, 可以增加或者修改远程仓库的配置
   3. 最后可以使用 -u 选项设置默认的关联, 后续就可以直接使用 git push 或者 git pull 进行代码推送和拉取

## 对于 origin
origin 是克隆下来仓库的一个默认的远程仓库的配置别名

* 自己创建的仓库
  * 是没有 origin 的默认别名的
  * git remote add origin http://github.com/longhudui/lhd-1.git
* 克隆回来的仓库
  * 是有一个 origin 的默认别名的



## 重点关注选手
1. 刘雨鑫       等lpl春季赛决赛-盲猜一手京东
2. 王世杰       打王者去
3. 李昕         top必胜






