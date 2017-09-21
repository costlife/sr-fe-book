欢迎来到仲畅git小课堂。<br/>
其实也没什么课堂不课堂，就是一些简单的指令。<br/>
由于现在分支挺多的，我们就先来看一下关于分支的指令。<br/>
```
git clone master(git地址)
```
** 先把代码clone下来**

```
git branch dev
```
** 生成一个名字叫dev的分支**

```
git checkout dev
```
** 切换到dev分支**

```
git push origin dev
```
** 把dev这个分支推送到远程仓库**<br/>

```
git branch -a
```
**看看有哪些小可爱呀**<br/>

```
git checkout -b dev
```
**表示创建并切换分支**<br/>

```
git checkout master
git merge dev
```
**把dev分支的工作成果合并到master分支上**<br/>
然后你就可以在dev这个分支上改一些bug，==再写一些更难被人发现的bug==出来。用完之后就要删掉啦。

```
git push origin --delete dev
```
**删除远程分支**

```
git branch –d dev
```
**删除本地已合并的分支**

```
git branch –D dev
```
**删除本地未合并的分支**<br/>
都删除啦，好啦，该下班了。哈哈哈，开个玩笑，修改之后肯定还要提交：

```
git status
```
**查看一下当前仓库的状态**<br/>
这里显示的状态可以告诉你现在代码处在什么状态，哪个文件有改动，有几次commit之类的东西。<br/>

```
git pull
```
**先更新一下代码**<br/>

```
git add .
```
**将所有修改过的文件提交到暂存区**<br/>

```
git add <file>
```
**将指定文件提交到暂存区**<br/>

```
git commit -m 'commit'
```
**commit里面不能是中文哈**<br/>

```
git commit -v
```
**提交时显示所有diff信息**<br/>

```
git push origin master
```
**把代码推送到master上**<br/>

版本回退：<br/>

```
git log
```

**查看日志**<br/>

```
git reset --hard HEAD^
```
**版本回退到上一个版本**<br/>
^代表几个版本，
```
^
```
是一个，^^是两个，如果比较多的话就可以写成*HEAD~100*

```
git reset --hard 2e70fdf
```
**版本回退到指定版本**<br/>



