### 基本的Linux命令

cd 改变目录

cd.. 回退到上一级目录

pwd 显示当前所在路径

ls(ll) 都是列出当前目录中的所有文件，只不过ll更为详细

touch 新建一个文件，如touch index.js 就会在当前目录下新建一个index.js文件

rm 删除一个文件，rm index.js就是删除index.js

mkdir 新建一个目录，就是新建一个文件夹

rm -r 删除一个文件夹，rm -r src 就是删除src目录

mv 移动文件，mv index.html src index.html是我们要移动的文件，src是目标文件夹，这样写必须在同一目录下

reset 重新初始化终端/清屏

clear 清屏

history 查看命令历史

help 帮助

exit 退出

#表示注释

![image-20211123101731722](git%E4%BD%BF%E7%94%A8.assets/image-20211123101731722.png)



git的工作流程：

1.在工作目录中添加，修改文件

2.将需要进行版本管理的文件放入暂存区域

3.将暂存区域的文件提交到git仓库

因此，git管理的文件有三种状态：已修改modified，已暂存staged，已提交committed

### 1.版本控制工具应该具备的功能

<ul>
    <li>协同修改</li>
    <li>数据备份</li>
    <li>版本管理</li>
    <li>权限控制</li>
    <li>历史记录</li>
    <li>分支管理</li>
</ul>

###  2.Git的优势

<ul>
    <li>大部分操作在本地完成，不需要联网</li>
    <li>完整性保证</li>
    <li>尽可能添加数据而不是删除或修改数据</li>
    <li>分支操作非常快捷流畅</li>
    <li>与linux命令全面兼容</li>
</ul>

### 3.本地库和远程库

#### 3.1本地库初始化

命令：

```linux
git init
```

效果：

![image-20211202102846177](git%E4%BD%BF%E7%94%A8.assets/image-20211202102846177.png)

注意： .git目录中存放的是本地库相关的子目录和文件，不要删除，也不要胡乱修改。

#### 3.2设置签名

形式：用户名：用户名

​            email:  邮箱

作用：区分不同开发人员的身份

辨析：这里设置的签名和登录远程库（代码托管中心）的账号，密码没有任何关系

命令：

<ul>
    <li>项目级别/仓库级别：仅在当前本地库范围内有效</li>
     git config user.name cxh <br>
     git config user.email 邮箱
    <li>系统用户级别：登录当前操作系统的用户范围</li>
    git config --global user.name cxh <br>
     git config --global user.email 邮箱
    <li>优先级：项目级别优先于系统级别，二者都有采用项目级别</li>
</ul>
#### 3.3基本操作

<ul>
    <li>状态查看操作</li>
    查看工作区和暂存区的状态<br>
    git status
    <li>添加操作</li>
    将工作区的“新建/修改” 添加到暂存区<br>
    git add 文件名
    <li>提交操作</li>
    将暂存区的内容提交到本地库<br>
    git commit -m "提交信息" 文件名
    <li>查看历史纪录操作</li>
    git log<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/git log.png"><br>
    多屏显示控制方式：<br>
    空格向下翻页<br>
    b向上翻页<br>
    q退出<br>
    git log --pretty=oneline<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/git log --pretty=oneline.png"><br>
    git log --oneline<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/git log --oneline.png"><br>
     git reflog<br>
    HEAD@{}指指针移动的次数<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/git reflog.png"><br>
    <li>查看历史记录操作</li>
    按索引值:<br>
    git reset --hard 索引值<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/git reset.png"><br>
    使用^符号(只能后退,一个^退一步):<br>
    git reset --hard HEAD^<br>
    使用~符号(只能后退，后退n步):<br>
    git reset --hard HEAD~n<br>
    reset三个参数对比:<br>
    git reset --soft:仅仅在本地库移动HEAD指针<br>
    git reset --mixed:在本地库移动HEAD指针,重置暂存区<br>
    git reset --hard:在本地库移动HEAD指针，重置暂存区和工作区<br>
    <li>删除文件并找回</li>
    前提：删除前，文件存在时的状态提交到了本地库<br>
    操作：git reset --hard 指针位置<br>
    &nbsp&nbsp删除操作已经提交到本地库：指针位置指向历史记录<br>
    &nbsp&nbsp删除操作尚未提交到本地库：指针位置使用HEAD<br>
    <li>比较文件差异</li>
    将工作区中的文件和暂存区进行比较：<br>
    git diff 文件名<br>
    将工作区中的文件和本地库历史记录进行比较：<br>
    git diff 本地库历史版本 文件名<br>
    不带文件名时比较多个文件<br>
</ul>

### 4.分支

#### 4.1分支的好处

<ul>
    <li>同时并行的推进多个功能的开发，提高开发效率</li>
    <li>各个分支在开发过程中，如果某一个分支开发失败，不会对其他分支有任何影响，失败的分支删除重新开始即可</li>
</ul>

#### 4.2分支操作

<ul>
    <li>创建分支</li>
    git branch 分支名<br>
    <li>查看分支</li>
    git branch -v<br>
    <li>切换分支</li>
    git checkout 分支名<br>
    <li>合并分支</li>
    第一步：切换到接受修改的分支（被合并，增加新内容）上<br>
    git checkout 被合并的分支名<br>
    第二步：执行merge命令<br>
    git merge 增加新内容的分支名
    <li>解决冲突</li>
    冲突的表现：<br>
    <img src="git%E4%BD%BF%E7%94%A8.assets/merge conflict.png"><br>
    冲突的解决：<br>
    第一步：编辑文件，删除特殊符号<br>
    第二步：把文件修改到满意的程度<br>
    第三步：git add 文件名<br>
    第四步：git commit -m "日志信息" （此时不能加文件名）<br>
</ul>

### 5.github的使用

#### 5.1创建账号

进入github首页创建账号即可

<img src="git%E4%BD%BF%E7%94%A8.assets/github.png">

#### 5.2创建远程仓库

##### 第一步：点击New repository

<img src="git%E4%BD%BF%E7%94%A8.assets/new repository.png">

###### 第二步: 填写项目名称，选择是否开源，即可创建。

<img src="git%E4%BD%BF%E7%94%A8.assets/create repository.png">

##### 第三步：复制仓库地址，创建别名

```linux
#查看远程地址别名
git remote -v
#添加远程地址别名
git remote add 别名(origin) 地址(https://github.com/cccccxhua/haha.git) 
```

<img src="git%E4%BD%BF%E7%94%A8.assets/repository.png">

#### 5.3 push :推送代码至远程仓库(只有团队成员能够push)

```
git push 别名(origin) 分支名(master)
```

<img src="git%E4%BD%BF%E7%94%A8.assets/push.png">

#### 5.4 clone :从远程仓库克隆代码至本地

```
git clone 远程仓库地址
#效果：
#1.完整的把远程仓库下载到本地
#2.创建origin 远程仓库别名
#3.初始化本地库
```

<img src="git%E4%BD%BF%E7%94%A8.assets/clone.png">

#### 5.5添加人员

<img src="git%E4%BD%BF%E7%94%A8.assets/add.png">

<img src="git%E4%BD%BF%E7%94%A8.assets/add1.png">

#### 5.6 pull:从远程仓库拉取代码

```
git pull 远程库地址别名 远程分支名
#pull = fetch + merge
git fetch 远程库地址别名 远程分支名
#git fetch 远程库地址别名 远程分支名 ：是将远程仓库的该分支拷贝下来，但此时与本地的代码无关，通过git checkout 远程库地址别名/远程分支名 可以进入拷贝过来的分支，查看代码，这些操作都不影响本地代码。
git merge 远程库地址别名/远程分支名 
#git merge 远程库地址别名/远程分支名 ：是将fetch下来的代码与本地代码合并
```

#### 5.7解决冲突

<ul>
    <li>如果不是基于Github远程库的最新版所做的修改，不能推送，必须先拉取</li>
    <li>拉去下来后如果进入冲突状态，则按照“分支冲突解决”操作即可</li>
</ul>

#### 5.8跨团队协作

第一步：点击fork,将远程库复制一份

<img src="git%E4%BD%BF%E7%94%A8.assets/fork.png">

第二步：将远程库代码克隆到本地

```
git clone 地址 分支名
```

第三步：本地修改，push到远程库

第四步：pull request 操作

<img src="git%E4%BD%BF%E7%94%A8.assets/pull request.png">

③点击 create pull request 

④发信息通知原远程库

⑤原仓库创建者，核实代码，merge pull request 

