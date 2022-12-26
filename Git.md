#### Git

```bash
# cd 进入文件夹 
git init  # 初始化仓库 
```

#### 配置用户名和邮箱

```bash
git config --global user.name "your name"  # user.name后面是空格
git config --global user.email "your email"

# 这个邮箱是方便同事或者网上的网友找到你 
# 如果是在公司内部使用，就用公司内部的邮箱 
# github / gitee 使用，随意

# 查看配置
git config --list --global
```

#### Git 

是一个分布式的版本控制系统   

version control system  VCS

1. 本地VCS
2. 集中式VCS  ====> SVN
3. 分布式VCS  ====> Git

Git主要作用：存档备份，多人协作开发。

#### Git区域

1. 工作区        红色
2. 暂存区        绿色 
3. 仓库            .git 文件

#### Git的一些常用操作

```bash
# 查看状态
git status
# 跟踪新文件 
git add 文件名 
git add .
# 做版本更新（提交）（记录存档）
git commit -m "描述信息"
# 跳过暂存直接提交
git commit -am "跳过暂存提交"
# 查看历史记录
git log --oneline 
# 查看所有的历史记录
git reflog 
# 回退版本
git reset --hard 提交的commitID
```

#### 将本地的更新，推送到远端仓库

```bash
# 推送之前 需要将本地仓库和远端仓库做一个关联
git remote add origin 'xxxxxx远端仓库地址'
git remote -v # 查看远端仓库的配置

SSH密钥对的模式 git@xxx    ===> 推荐使用密钥对
HTTPS模式    https
```

#### 密钥对的配置 

```bash
https://gitee.com/help/articles/4181#article-header0
# 1. 执行这一句
ssh-keygen -t ed25519 -C "xxxxx@xxxxx.com"  写自己的邮箱
# 按三次回车 （yes）

# 2. 查看密钥对
cat ~/.ssh/id_ed25519.pub
# 拿到我们的公钥 配置到gitee或者github上

# 3. 验证是否配置成功
ssh -T git@gitee.com
# 如果出现了 successfully

# 4. 添加远端仓库 
git remote add origin git@gitee.com:vrfe/demo-git.git
# 注意，上面添加远端仓库关联的地址，要填自己的仓库

# 如果出现remote origin already exists
# 先把它移除掉 
git remote rm origin 

# 重新执行上述的代码
git remote add origin git@gitee.com:vrfe/demo-git.git

# 这个时候，就可以执行推送  
第一次推送
git push -u origin master

# 有时候，推送不成功，会报错 ，当远端仓库和本地仓库不一致的时候。
git push -u origin master -f  # 强制推送，让本地的仓库，覆盖掉远端的仓库。
-f 表示 force ==> 强制推送的意思。
```



```bash
git status 
git add . 
git commit -m "msg"
git push 
# 之后的每一次推送，直接使用git push就好了 

# 公司里，几个同学都在推送到master分支，远端仓库的代码就会和本地不一致。需要git pull 拉取最新的更新

git pull 拉取了 会把最新的更新，同步到本地的仓库中。
```



### branch分支 

```js
git branch 

git merge 
```

