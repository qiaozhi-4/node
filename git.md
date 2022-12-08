### 项目流程

1. git init		初始化本地库
2. git status		检查是否有未追踪的(是否有未提交的)

3. 
   - 不干净,
     1. git add 文件名		把所有的文件添加到暂存区
     2. git commit  -m "日志信息"		提交到本地仓库
   - 干净
     1. git commit "日志信息"

4. 创建新分支
   - git checkout -b login	-- login 是分支名,一般创建新模块时创建新分支,完成之后合并到主分支
   - 





### git常用命令

| 命令                               | 介绍                                                      |
| :--------------------------------- | --------------------------------------------------------- |
| git init                           | 初始化本地库                                              |
| git status                         | 是否有未追踪的                                            |
| git add 文件名                     | 把指定文件添加到暂存区                                    |
| git rm --cached 文件名             | 把指定文件从暂存区删除                                    |
| git commit -m "日志信息"           | 提交到本地仓库                                            |
| git commit -m "日志信息" 文件名    | 提交指定文件到本地仓库                                    |
| git reflog                         | 查看日志                                                  |
| git log                            | 查看详细日志                                              |
| git reset --hard 9199de9           | 切换到 9199de9  这个版本                                  |
| git branch 分支名                  | 创建分支                                                  |
| git branch -v                      | 查看分支                                                  |
| git checkout 分支名                | 切换分支                                                  |
| git merge 分支名                   | 把指定的分支合并到当前分支上                              |
| git remote -v                      | 查看当前所有远程地址别名                                  |
| git remote add 别名 远程地址       | 给远程地址起别名                                          |
| git push 远程库地址别名 分支名     | 推送本地分支上的内容到远程仓库                            |
| git clone 远程地址                 | 将远程仓库的内容克隆到本地                                |
| git pull 远程库地址别名 远程分支名 | 将远程仓库对于分支最新内容拉下来后与 当前本地分支直接合并 |
| git clone 远程地址                 | 克隆远程仓库到本地                                        |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |
|                                    |                                                           |

​        



​        







### 提交被拒绝

 切换到自己项目所在的目录，右键选择GIT BASH Here ，然后依次输入

1. git pull 
2. git pull origin master 
3. git pull origin master --allow-unrelated-histories 
4. git push -u origin master





git init                           //初始化仓库

```java
https://gitee.com/georgedbddbbd/baiyun
```

git add .(文件name)                //添加文件到本地 
git commit -m “first commit”      //添加文件描述信息
git remote add  origin 远程仓库地址 //链接远程仓库 

```java
git remote add origin https://gitee.com/georgedbddbbd/baiyun
```

git pull origin 仓库分支名      // 把本地仓库的变化连接到远程仓库master                                     分支

```java
git pull origin master     
```

git push -u origin 仓库分支名        //把本地仓库的文件推送到远程仓库master    

```java
git push -u origin master
```




