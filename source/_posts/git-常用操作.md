title: "git 常用操作"
date: 2016-07-30 15:42:49
tags: git
---
###拉代码
```bash
git clone ssh://user-name@url
```
####获取远程信息
```bash
git fetch (--all)
```
#### 更新代码
```bash
git pull (--rebase| -r)
//(pull 表示把远程仓库的更新拉下来， --rebase 虽然是可选项， 但是一般都建议一起使用，这里涉及到 “基”的概念。
```
###分支
#### 切分支
代码拉下来后默认是在master分支， 需要用 ``git checkout ref_name ``切过去
####列分支
``git branch`` 列出本地分支
``git branch -r``列出远程分支
#### 切分支
``git checkout branch_name` ` （执行命令前本地不能有未缓存的提交，否则失败）
#### 新建分支
```bash
git branch 'branch_name'
git checkout -b 'branch_name'  // 执行完后会立即切换到新分支
git branch 'branch_name' 'origin/branch_name' //新建远程分支 
git checkout branch_name (等价于 git checkout  -b 'branch_name'  'origin/branch_name' )
//使用远程分支，并在本地建立branch
```

#### 删除本地分支
```bash
git branch -D 'branch_name' //大写D表示强制删除
```

#### 本地分支与远程分支的对应
特殊情况下，执行 ``git pull`` 命令时会提示找不到对应的远程分支， 需要用 ``git branch --set-upstream-to=<upstream>``命令指定一个远程分支.
####显示远程分支的url
```bash
//if referential integrity has been broken:
git config --get remote.origin.url

//If referential integrity is intact:
git remote show origin
```
###提交
####本地提交
- 一般都用图形化工具 citool.用``git citool``命令可调起。
- 命令行的方式：

```bash
 git add // 把文件加到版本库的管理中 ，执行完后文件在缓存区
 git add --all //将所有文件放入stage中，包括新增加的文件
 git rest // unstaged all files
 git commit -m 'msg' //将stage中文件提交
 git commit -am 'msg' //将modify和 stage 中文件提交，不包括不在stage中的新增文件
 git commit --amend -m‘msg’ 将本次提交和上次提交合并。在本地的提交中使用，还没有push到服务器中
```
#### 推送到服务器
```bash
git push 
git push origin HEAD:branch_name //本地分支名与远程名称不对应时候
git push origin HEAD:refs/for/ref_name //推送到gerrit
```

注意1：HEAD在LINUX下需要大写
注意2： 不要忘记加 HEAD:refs/for/ 否则有可能会创建一个新分支。

#### 冲突的解决
命令：
```bash
git mergetool 'file_path'
```
####git 对比

```bash 
git difftool --dir-diff(-d) //git open all diff files 
git difftool -d HEAD //stage 中files对比
git difftool -d sha sha^1 // 提交sha的文件变更
``` 
### git svn
```bash
git svn  fetch // 更新svn代码
git svn rebase //更新本分支head到最新
```
###tag
#### 打tag
命令：

```bash
git tag V_1.0.0.0 -m “version 1.0”
```
一般每编一次发布版，都会打上一个tag
#### 将tag推送到远程
```bash
git push origin tag_name
```
注意： 推送到远程的TAG必须得有日志信息，对应于上面 -m 参数后的内容。
###gitk使用
查看分支

```bash
gitk // 查看当前本地分支
gitk ref_name //查看其他分支
gitk origin/ref_name //查看某个远程分支
gitk --all //查看所有分支
```
###本地修改


####常用命令
```bash
git reset [--hard|--soft|--mixed] [revision] //reset命令只对入库的文件有效，
git clean –fd //对未入库的文件，可使用 git clean –fd 清除
git reset --hard //回退所有的内容

//可以回退某一个提交，这个操作相当于是把当时那个提交逆向PATCH了一次。
//操作完成后，需要COMMIT到仓库。
git revert –n sha1-id
//回退某一次的提交某一个文件
git checkout sha1-id file (file1...)


```
####git stash
```bash
//工作到一般时有紧急任务时， 配合 
git stash
git stash pop
git stash save -m'log'
git stash -p //stash 某一文件
// y - stash this hunk
// n - do not stash this hunk
// q - quit; do not stash this hunk or any of the remaining ones
// a - stash this hunk and all later hunks in the file
// d - do not stash this hunk or any of the later hunks in the file
// g - select a hunk to go to
// / - search for a hunk matching the given regex
// j - leave this hunk undecided, see next undecided hunk
// J - leave this hunk undecided, see next hunk
// k - leave this hunk undecided, see previous undecided hunk
// K - leave this hunk undecided, see previous hunk
// s - split the current hunk into smaller hunks
// e - manually edit the current hunk
// ? - print help// 
git stash clear // delete all stashes at once
```


####git 提取patch.
1. 可以先使用git citool本地提交。
2. git format-patch -w head~1 
3. 使用 git reset --hard 撤销本地提交.
4. 使用gitk查看是否撤销本地提交。
5. 应用patch.
```bash
git diff --binary > xxx.patch //生成patch
git apply xxx.patch   //好用
git am xxxxxx.patch   //不好用.
```

####git 回退
```bash
git reset HEAD~1
git reset HEAD^
```
（master分支向前回退一个提交。gqg:回退本地提交，恢复到提交前更改状态, 或者用:git reset HEAD~1  ~1表示回退一次提交，~N表示回退N次提交）.

- 只要有.git目录 就可以使用git reset --hard 把代码恢复出来。

####git 修改只有大小写区别的文件
```bash
git mv (--force) myfile MyFile
(mv: allow renaming to fix case on case insensitive filesystems)
```

#### revert某个提交:
1. 使用gitk, 查看要revert的提交，把SHA1 ID复制下来.
2. git revert -n xxxxxxxxxxxxxxxxxxxxxxxxxxxx 
3. git citool 提交然后push.

#### cherry pick
```bash 
git cherry-pick "branch_name"  //cherry pick "branch_name" 最上方修复，并提交
git cherry-pick "sha-id"  //cherry pick 某一次提交
```
#### 回退制定版本
```bash
git checkout 'SHA' //回退到制定'sha'值
```
###git 配置
1. 修改git默认的编辑器nano为vim的方法``git config --global core.editor vim``
2. 指定全局 ignore 文件 ``git config --global core.excludesfile  '/Users/xx/.gitignore_global' ``