#ssh-keygen

生成管理和转换认证密钥，包括rsa和dsa两种密钥。
会创建一对密钥，xxx和xxx.pub。xxx代表私钥，xxx.pub代表公钥。公钥需要放在服务器端。

##参数

[详细参数](http://killer-jok.iteye.com/blog/1853451)

+   -b
    指定密钥长度。
    对于rsa，最小768位，默认2048位。
    对于dsa，必须是1024位。

+   -t
    密钥类型。有rsa和dsa两种。

+   -C
    提供注释。

+   -f
    指定密钥文件名。

##应用

```
#得到两个文件，id_rsa_aaa和id_rsa_aaa.pub
#会要求输入密码，不用密码直接回车
ssh-keygen -t rsa -f id_rsa_aaa -C “xxx@gmail.com”
```