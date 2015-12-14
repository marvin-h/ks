#git log

查看提交历史
q退出查看

##命令

###-p

显示内容差异

```
git log -p
```

###-n

查看最近n次更新

```
git log -2
```

###--stat

显示增删改的行数

```
git log -1 --stat
```

###--since | --after

指定时间之后的提交

###--until | --before

指定时间之前的提交

###--author

指定特定修改者的提交

###--committer

指定特定提交者的提交