#git config

配置git环境变量

##配置级别

有三种级别：

+   --local
    
    仓库级别
    配置文件位于仓库目录下的.git/config

+   --global

    用户级别
    配置文件位于

    +   ~/.gitconfig (linux)
    +   C:\Users\user\\.gitconfig (windows)

+   --system
    
    系统级别
    配置文件位于

    +   /etc/gitconfig (linux)
    +   C:\Program Files (x86)\Git\etc\gitconfig (windows)


优先级：local > global > system


##命令

###--list

列出git配置信息

```
git config --list
git config --global --list
```

##环境变量

###查看环境变量

git config [--local | --global | --system] attrname

```
git config user.name
git config --global user.name
```

###设置环境变量

git config [--local | --global | --system] attrname attrvalue

如果没有指定配置级别，默认使用--local

```
git config user.name john
git config --global user.name john
```

###user.name

用户名

###user.email

电子邮箱

###http.proxy

设置http/https代理

```
git config --global http.proxy host:port
git config --global https.proxy host:port
```
