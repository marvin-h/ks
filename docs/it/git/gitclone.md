#git clone

克隆远程仓库到本地

##命令

git clone url

```
git clone git@github.com:marvin-h/test.git
```

git clone url directoryName

重命名目录

```
git clone git@github.com:marvin-h/test.git test1
```

##git协议

四种传输协议：

+   本地协议

    ```
    git clone /opt/git/proj.git
    ```

+   ssh协议

    数据的传输都是加密和授权的
    高效，传输之前压缩数据
    可控制写权限
    
    ```
    git clone ssh://user@server:proj.git
    ```

+   git协议

    需要开放9418端口
    传输最快的协议
    缺少授权机制

    git://

+   http/s协议

    http(s)://


如果不指定协议，默认使用ssh协议
git/http(s)只有读权限，ssh有读写权限

