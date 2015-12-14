#git remote

操作远程仓库

##命令

###git remote

查看远程仓库的shortname

###git remote -v

查看远程仓库的shortname和url

###git remote add shortname url

添加远程仓库，相当于指定本地仓库与远程仓库的关联信息

```
git remote add mypb git://github.com:john/proj.git
```

###git remote show shortname

查看远程仓库信息

###git remote rename oldshortname newshortname

修改远程仓库的shortname

###git remote rm shortname

移除远程仓库信息，移除的是本地仓库与远程仓库的关联信息

