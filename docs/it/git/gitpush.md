#git push

将本地仓库的更新推送到远程仓库

##命令

###git push shortname branch

将本地仓库的branch分支推送到远程仓库shortname的branch分支

```
git push origin master
```

###git push shortname localbranch:remotebranch

将本地仓库的localbranch分支推送到远程仓库shortname的remotebranch分支

###git push shortname :branch

删除远程分支

```
git push origin :master
```