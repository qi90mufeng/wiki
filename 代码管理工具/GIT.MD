## 问题1：如何撤销commit

#### --mixed 

意思是：不删除工作空间改动代码，撤销commit，并且撤销git add . 操作

这个为默认参数,git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

 

#### --soft  

git reset --soft HEAD^

git reset --soft  3d49864494bbacd0aa019a17c6ccfdaa3a56ec01

不删除工作空间改动代码，撤销commit，不撤销git add . 

 

#### --hard

git reset --hard  4fd80b2706684fed7dad0c0d425b523e797c391d

删除工作空间改动代码，撤销commit，撤销git add . 

注意完成这个操作后，就恢复到了上一次的commit状态。



## 问题2：如何修改commit的注释

 git commit --amend