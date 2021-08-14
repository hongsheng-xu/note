# Git版本控制管理

## 初始化项目

`git init`

## 配置

### 查看配置

`git config -l`

### 移除设置

`git config --unset [--global] 设置项`

### 配置用户信息

`git [--global] config user.name '用户名'`

`git [--global] config user.email '邮箱地址'`  *--global全局配置*

### 配置文件

git配置文件

`项目/.git/config`

项目git配置文件

`项目/.gitconfig` *该设置拥有最高优先级*

linux下配置文件

`/etc/gitconfig`

### 配置别名

`git config --global 别名 '命令1 参数'`

## 创建版本库副本

`git clone 仓库名` `git clone ssh链接|https链接`

##  添加文件到版本库

### 添加文件夹

`git add 文件夹`

### 添加文件

`git add 文件名.文件后缀`

### 添加所有

`git add *`	*暂存一个文件文件的状态从未追踪变为已追踪*

*tips: git是基于SHA散列计i算对象内容,git追踪的是内容而不是文件如果两个文件内容完全一样,git在对象库只保存一份blob'如果文件发生了变化git会重新计算一个新的SHA1值然后替换原来的blob对象git存储的是文件的每个版本而不是差异git以一个文件的内容的散列值作为文件名*

## 版本库文件修改

## 文件删除

`git rm [--cached] 文件名`	*--catched会删除索引的文件并将其保留在工作目录中,git rm会将其文件从索引和工作目录中都删除*

*tips:文件更改后需要重新提交*

### 文件重命名

`git mv 文件1 文件2`

*tips:文件更改后需要重新提交*

### 文件内容读取

`git cat-file -p 散列值`

**使用`git rev-parse 散列值开始部分`获取到完整的40长度散列值**

## 状态管理

`git staus`

## 提交

### 提交单个文件

`git commit 文件名.文件后缀`

### 提交所有

`git commit -m '提交说明' `	*--message*

`git commit -a` *--all选项会自动提交所有未暂存的和未追踪的文件*

*tips: git不会处理空文本提交*

## 查看提交

### 查看历史提交

`git log` `git show-branch [--more=查看提交次数]`

> commit a15c88e2cb0c5fca3b322257

*tips:a15c88e2cb0c5fca3b322257为提交码*

### 查看单次提交

`git show 提交码`

`git show --pretty=fulller` *查看提交的其它细节*

### 查看提交差异

`git diff 提交码1 提交码2`

## Git原理

### Git追踪内容

​	Git的内容追踪主要表现为两种关键的方式,git的对象库基于对象内容的散列计算值,而不是基于用户原始文件布局的文件名或者目录名设置,因此当git放置一个文件到对象库中的时候,它基于数据的散列值而不是文件名.

​	如果两个文件内容完全一样,无论是否在相同目录,Git在对象库里只保存一份blob形式的内容副本*Git是基于文件内容计算每一个文件的SHA1值然后将blob对象放到对象库里并以SHA1值作为索引*

​	如果这些文件发生了一些变化,Git会为它计算一个新的SHA1值然后识别出它现在是一个新的blob对象,并将它加入到Git对象库中,原来的blob在对象库中保持不变

​	其次文件从一个版本变化到另一个版本,Git内部的数据库有效地存储每一个文件的每一个版本而不是差异因为Git使用一个文件的全部内容的散列值作为文件名,所以Git必须对每一个文件的完整副本进行操作.Git不能将工作或者对象库条目建立在文件内容的一部分或者文件的两个版本的差异之上.

**Git索引机制: .git/objects/hash/树对象内容 Git数据存储: blob对象/树对象**

Git的物理数据布局并不模仿用户的文件目录结构相反Git有一个完全不同的结构却可以重建用户的原始布局,Git内部

### Git打包文件

​	Git使用了一种叫做打包文件(package)的更有效的存储机制,要创建一个打包文件Git首先定位内容非常相似的全部文件,然后为它们之一存储整个内容,之后计算相似文件之间的差异并且只存储差异

​	Git维护打包文件表示中每个完整文件(包括完整的内容的文件和通过差异重建出来的文件)的原始blob的SHA1值,这给定位包内的对象索引机制提供了基础

### Git对象库图示

​	blob对象是数据库结构的底端,它什么也不引用而且只被树对象引用

​	树对象指向对个blob对象,也可以指向其它树对象

​	每个提交对象指回它的一个或多个父提交: 数据流从父提交流向子提交

![对象库](https://images-1300732204.cos.ap-chengdu.myqcloud.com/14310957-3fdce556428c8596.png)

![提交后的](https://images-1300732204.cos.ap-chengdu.myqcloud.com/14310957-9539ae06bcc80e07.png)

![](https://images-1300732204.cos.ap-chengdu.myqcloud.com/14310957-6a1e362e5d7cf1e5.png)

![](https://images-1300732204.cos.ap-chengdu.myqcloud.com/14310957-a8e69d240b7b1a50.png)

### Git文件

​	Git通过目录树的对象来追踪文件的路径名,当使用`git add`命令时Git会给添加的每一个文件的内容创建一个对象,但它并不会马上成为树创建一个对象,相反索引更新了,索引位于`.git/index`中,它跟踪文件的路径名和相应的blob每次执行命令(如:git add|rm|mv)时Git会用新的路径名和blob'信息来更新索引

#### 查看文件关联

`git ls-files -s`

#### 查看树

`git write-tree`

`git cat-fille -p 散列值4位以上`

#### 提交树对象

`git commit-tree 散列值`

#### 创建标签

`git tag -m '提交信息' 标签 散列值`

`git rev-parse 标签` *查看标签对象*

​	标签指向提交对象,通常情况下git通过某些分支来给特定的提交命名标签Git通常给指向树对象的提交对象打标签,这个树对象包含版本库中文件和目录的整个层次结构的总状态

### Git文件分类

​	已追踪的(Tracked): 在版本库中或已暂存到索引中的文件

​	被忽略的(Ignored): 必须在版本库中被明确声明为不可见或被忽略

​	未追踪的(Untracked): Git将工作目录下的所有文件作为一个集合减去已追踪的和被忽略的,剩下的就是为追踪的文件

### Git文件管理

