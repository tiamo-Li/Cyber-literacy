[toc]

# 1. VScode免密SSH登录

## 1. 生成RSA密钥

（如果已有RSA密钥，则直接进行进行步骤2）

打开shell终端，输入命令，生成密钥对

```bash
ssh-keygen -t rsa -b 4096
```

如果你是第一次生成密钥对，那么一路回车就可以了

在你的用户名~~（我的用户名是JingHong）~~下会生成密钥对，即在 `C:\Users\JingHong\.ssh` 下存在 `id_rsa` 和 `id_rsa.pub` 两个文件，分别是私钥和公钥

## 2. 上传公钥

假设你要登陆的服务器权限为root，那么我们可以先将 `id_rsa.pub` 文件放到 `/root/` 下

然后创建 `.ssh` 文件夹

```bash
mkdir -p ~/.ssh
```

在 `.ssh` 下创建并修改 `authorized_keys` 文件，将 `id_rsa.pub` 的内容追加到 `authorized_keys` 文件中

```bash
cat id_rsa.pub>> ~/.ssh/authorized_keys
```

删除其他组和其他的修改权限

```bash
chmod -R go= ~/.ssh
```

## 3. 添加私钥验证

在VScode中修改ssh配置文件，即在 `.ssh` 文件夹下的 `config` 文件

在已经配置了公钥的服务器下添加 `IdentityFile` 项，其后添加私钥的地址

```
Host Atlas-200I-DK-A2
    HostName 192.168.137.100
    User root
    IdentityFile "C:\Users\JingHong\.ssh\id_rsa"
```

