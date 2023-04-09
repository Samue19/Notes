# git

git config -l 查看git配置

git config --system --list 查看系统配置

git config --global --list 查看全局配置

![image-20220901090518363](C:\Users\samue\AppData\Roaming\Typora\typora-user-images\image-20220901090518363.png)

![image-20220901090604720](C:\Users\samue\AppData\Roaming\Typora\typora-user-images\image-20220901090604720.png)

git init	初始化.git 文件

git clone url

![image-20220901093114887](C:\Users\samue\AppData\Roaming\Typora\typora-user-images\image-20220901093114887.png)

git status  查看文件状态

git add .  添加所有文件到暂存区

git commit -m 提交暂存区中的内容到本地仓库 -m 提交信息

![image-20220901093133170](C:\Users\samue\AppData\Roaming\Typora\typora-user-images\image-20220901093133170.png)

ssh 登录

ssh-keygen -t rsa

克隆到本地



git branch 列出所有本地分支

git branch -r 列出所有远程分支

git branch [branch-name] 新建一个分支，但仍停留在当前分支

git checkout -b [branch] 新建一个分支，切换到该分支

git merge [branch] 合并指定分支到当前分支

git branch -d [branch-name] 删除分支

git push orgin --delete [branch-name] 删除远程分支

git branch -dr [remote/branch] 删除远程分支



**常用操作**

```shell
git config --global user.name 用户名	# 设置用户名
git config --global user.email 邮箱	 # 设置用户签名
git init							 # 初始化本地库
git status							 # 查看本地库状态
git add	文件名							# 添加到暂存区
git commit -m "日志信息" 文件名		 # 提交到本地库
git reflog							 # 查看版本记录
git log								 # 查看版本详细记录
git reset --hard 版本号				# 版本穿梭 
```

**分支操作**

```shell
git branch 分支名					# 创建分支
git branch -v					  # 查看分支
git checkout 分支名				# 切换分支
git merge 分支名					# 把指定分支合并到当前分支
```

**远程库**

```shell
git remote -v				# 查看本地远程库别名
git remote add HuYun xxx    # 添加远程库的别名
git push HuYun master		# 推送master分支
git pull HuYun master		# 拉取分支
```

**ssh**

```shell
# 创建rsa密匙
ssh-keygen -t rsa -f ~/.ssh/acwing_rsa -C "2769461869@qq.com"
# 清空ssh缓存
ssh-add -D
ssh-add acwing_rsa
# 测试连接
ssh -T git@git.acwing.com
```



![image-20220901101122027](C:\Users\samue\AppData\Roaming\Typora\typora-user-images\image-20220901101122027.png)

