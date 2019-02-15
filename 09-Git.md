# Git
***
* Git：分布式版本管理系统
  * 详细指南：https://backlog.com/git-tutorial/cn/
  * 学习要点：
    * `gitFlow`
    * `aster`
    * `developer`
    * `hotfix`
    * `release`
    * `feature`
    * `branch`
  * 一句话理解Git(面试专用)
    * Git的每个分支的管理类似于链表，
    每次提交都会产生一个SHA1（安全哈希算法）的唯一标识符。
    此唯一标识符是引用的指针。
    后续的增删改查操作都可以基于这个指针进行索引操作。
    * 关键字：分布式，四个分区，链表，SHA1指针
* 数据库
  * 远程数据库：配有专用的服务器，为了多人共享而建立的数据库
  * 本地数据库：为了方便用户个人使用，在自己的机器上配置的数据库。
* 分支：branch
  * 分支是为了将修改记录的整体流程分叉保存。分叉后的分支不受其他分支的影响，所以在同一个数据库里可以同时进行多个修改。
  * 创建分支：`git branch <branchname>`
  * 切换分支：`git checkout <branch>`
  * 创建并切换分支：`git checkout -b <branch>`
  * 合并分支：
    * 在主分支master合并名为commit的分支：`git merge <commit>`
    * 当前分支合并主分支master：`git rebase master`
  * 删除分支：`git branch -d <branchname>`
* 分支主要分类：
  * master分支：一般会已此分支为主分支（发布分支）。
    主分支的意思是说开发者不会在主分支上开发， 主分支只接受外分支的合并。合并完之后，验证通过，打tag上线。
  * develop分支：作为日常开发分支，
    同时会有多人在上面提交代码，为了保证提交不冲突，尽量保证模块拆解合理，开发没有同时修改同一文件的情况。
  * feture分支：这些分支是发布之后的bug修复分支，
    不同开发者产生的Bug，会不同分支上修复bug，最终合并到master分支上上线。
  * 图例：
  ![](/images/分支分类.jpg "分支分类")
* 四个分区：
  * 工作区
  * 暂存区
  * 本地分支
  * 远端分支
  * 图例：
  ![](/images/git四个工作区.jpg "git四个工作区")
* Git配置
  * 修改用户信息
    * `git config --list`                                   // 配置信息列表
    * `git config --global user.name "John Doe"`            // 设置用户名
    * `git config --global user.email johndoe@example.com`  // 设置邮箱
  * 设置不同的仓库源
    * `git remote --help`               // 查看帮助
    * `git remote`                      // 查看不同源
    * `git remote add [name] [url]`     // 添加不同地址的源，并取一个别名
    * `git remote remove [name]`        // 删除一个源
* 基本操作
  * 仓库基本操作：
    * `git init`                      // 在当前目录新建一个Git代码库
    * `git init <project-name>`       // 新建一个目录，将其初始化为Git代码库
    * `git clone <git-hub-url>`       // clone git仓库
    * `git clone <url> -b <branch>`   // [高阶用法] clone git仓库并且制定分支
  * 操作完整提交流程：
    * `vi readme.md`              // 修改readme文件，文件在工作区
    * `git add readme.md`         // 文件进入缓存区，缓存区的文件可以被checkout移除到工作区
    * `git commit 'add readme'`   // 文件进入提交分支，但还是在本地
    * `git push origin master`    // 提交分支 push 到远端分支
  * 操作完成更新流程
    * `git pull : git fetch + git merge`          // 分支有两条提交线合并，并且多出了新的提交节点
    * `git pull —rebase: git fetch + git rebase`  // 分支合并在同一条提交线上
* 提交信息检查
  * `git diff`                              // 查看当前工作区改动点
  * `git diff commit_hash1 commit_hash2`    // 提交hash1和hash2的差异
  * `git diff branch_a branch_b`            // 分支a和b的差异
  * `git status`                            // 当前改动文件
  * `git log`                               // 查看提交历史
  * `git log --pretty=oneline`              // 提交历史缩减一行查看，主要是提交Hash值
* 分支管理
  * `git checkout -b daily/0.0.1`       // 已当前分支为基础，创建daily/0.0.1分支
  * `git branch -la`                    // 查看本地分支及远端分支
  * `git branch -D [branchName]`        // 强制删除本地分支
  * `git branch -d [branchName]`        // 删除已经Merge过的分支
  * `git checkout -b daily/0.0.1`       // 创建一个分支
  * `// 如何删除远端多余分支
  * `git push -delete <remote_name> <branchName>` // 大多数情况remote_name为origin
* 代码合并三种方式
  * merge
  * cherry-pick
  * patch
  * 图例：
  ![](/images/git代码合并.jpg "git代码合并.jpg")
* 如何使版本信息回退到某次提交？revert 和 reset有什么区别？
  * `git revert`： 撤销某次操作，此次操作之前的commit都会被保留。
  * `git reset`： 撤销某次提交，但是此次之后的修改都会被退回到暂存区。
    * 强制回退到某次提交，且需要强制提交
      * `git reset ——hard commit_hash`
      * `git push origin master --force` 
    * 回退到某提提交，保存提交commit记录, 重新commit
      * `git revert commit_hash`
      * `git add .`
      * `git commit -m "revert"`
      * `git push origin master`
* 如何创建Tag，如何以某个Tag创建分支
  * 创建tag
    * `git tag -a daily/0.0.1 -m "add develop file"` // 创建标注标签
    * `git tag daily/0.0.1` // 简单创建tag
  * 分享tag到远端
    * `git push origin [tagname]`
    * `git push origin --tags` 
  * 如何已某个tag创建分支
    * `git checkout -b <newbranch> <tagname>`
  
  
