# GPG

## 什么是GPG

1. GPG是GNU Privacy Guard的缩写, 他是一种基于密钥的加密方式，使用了一对密钥对消息进行加密和解密， 来保证消息的安全传输。
2. GPG有许多用途， 主要用于文件加密， yum安装软件包的时候会使用gpg来加密验证

## 安装

1. 下载源码, 编译安装

   ```shell
   ./configure
   make
   make install
   ```

2. 二进制包管理安装

   ```shell
   sudo apt-get install gnupg
   yum install gnupg
   ```

## 生成密钥

1. 安装成功后，可以使用`gen-ken`参数生成自己的密钥
   * `gpg --gen-key`
2. 创建密钥步骤
   1. 系统会询问选择加密算法, 默认为RSA密钥
   2. 系统会询问密钥长度，越长越安全(默认2048)
   3. 设定密钥的有效期， 默认永不过期
   4. 输入个人信息
      * 需要用户表示辨认密钥， 本软件使用真实姓名， 注释和电子邮件组合地址。
      * 注释可以为空
   5. 系统提示设定私钥密码，为了防止误操作，或者系统入侵时有人擅自动用密钥
   6. 系统提示，执行随机事件， 获取更多随机操作
   7. EDDD6D76(用户IDhash字符串)， 提供随机密钥生成
   8. 最好生成一张撤销证书， 以备密钥作废， 可以请求外部公钥服务器撤销公钥
      * `gpg --gen-revoke [用户ID]`

## 密钥管理

### 列出密钥

1. 列出密钥

   * `list-keys`: 参数为列出系统中已有的密钥

   * `gpg --list-keys`

   * 结果显示

     ```bash
     /home/lcwspr/.gnupg/pubring.gpg		# 显示公钥文件名(pubring.gpg)
     -------------------------------
     pub 4096/EDDD6D76 2014-08-11		# 第二行显示公钥特征(4096, hash字符串和时间戳)
     uid Ruan yi <yi.163.com>		# 显示用户ID
     sub 4096/3FA698E4 2014-08-11		# 显示私钥特征
     ```

2. 删除密钥

   * `gpg --delete-key [用户ID]`

### 输出密钥

1. 公钥文件(.gnupg/pubring.gpg)以二进制文件形式存储， armor参数可以将其转换为ASCII码显示
   * `gpg --armor --output public-key.txt --export [用户id]`
   * 用户ID指定那个用户公钥， output参数指定输出文件名(public-key.txt)
2. 类似的， export-secret-keys可以转换私钥
   * `gpg --armor --output private-key.txt --export-secret-keys`