#ssh

[secure shell，安全外壳协议](http://baike.baidu.com/link?url=DWY5n4oFB6j435yljVlmQjuQ6Bvzvp0I8h91FXozwTfyzrvlhn7D5FwP5xHmmQs2trguBxPUPwCGZYo0jBBWwog1bLTX_6T5Ut9aopynefy)

##目录

linux:

`~/.ssh`

windows:

`C:\Users\username\.ssh`

##创建密钥

[ssh-keygen](ssh-keygen.md)

可创建多对密钥

##config

可配置多个ssh key

+   host
    主机别名，可以随意配置。可使用通配符。
    当使用ssh时候，如果server的url能匹配host的值，则使用hostname的url

+   user
    用户名

+   port
    端口，默认是22。

+   hostname
    主机名，server真实的url

+   identityfile
    密钥文件

```
#github配置
host github.com
    user git
    port 443
    hostname ssh.github.com
    identityfile ~/.ssh/id_rsa

#git oschina配置
host git.oschina.net
    user git
    port 443
    hostname git.oschina.net
    identityfile ~/.ssh/id_rsa_git_oschina
```

```
ssh git@github.com
ssh git@git.oschina.net
```