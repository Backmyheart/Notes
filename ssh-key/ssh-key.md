# SSH-Key

## 首先需要检查电脑是否已经有SSH key

`cd` 到用户主目录：  

	cd ~

查看用户主目录下是否有 `.ssh` 目录:  

	ls -l

如果有 `.ssh` 目录，再看看这个目录下有没有 `id_rsa` 和 `id_rsa.pub` 这两个文件。

---

## 创建一个SSH key

执行命令：  

	ssh-keygen -t rsa -C "zhulei@kylinos.cn"  

代码参数含义：  

```shell
-t ：指定密钥类型，默认是rsa，可以省略
-C ：设置注释文字，比如邮箱
-f ：指定密钥文件存储文件名
```

以上代码省略了 `-f` 参数，因此，运行上面那条命令后会让你输入一个文件名，用于保存刚才生成的 `SSH key` 代码，如：

```shell
Generating public/private rsa key pair.
# Enter file in which to save the key (/c/Users/you/.ssh/id_rsa): [Press enter]
```

当然，也可以不输入文件名，使用默认文件名（推荐），那么就会生成 `id_rsa` 和 ` id_rsa.pub` 两个秘钥文件。  

接着又会提示你输入两次密码（该密码是你`push`文件的时候要输入的密码，而不是`github`管理者的密码）。  

当然，你也可以不输入密码，直接按回车。那么`push`的时候就不需要输入密码，直接提交到`github`上了，如：

```shell
Enter passphrase (empty for no passphrase): 
# Enter same passphrase again:
```

接下来，就会显示如下代码提示，如：  

```shell
Your identification has been saved in /c/Users/you/.ssh/id_rsa.
# Your public key has been saved in /c/Users/you/.ssh/id_rsa.pub.
# The key fingerprint is:
# 01:0f:f4:3b:ca:85:d6:17:a1:7d:f0:68:9d:f0:a2:db your_email@example.com
```

当你看到上面这段代码的收，那就说明，你的 `SSH key` 已经创建成功，你只需要添加到`github`的`SSH key`上就可以了。

---

## 添加 SSH key 到 github 上面去

首先你需要拷贝 `id_rsa.pub` 文件的内容，你可以用编辑器打开文件复制，也可以用`git`命令复制该文件的内容，如：  

	clip < ~/.ssh/id_rsa.pub

登录你的`github`账号，从右上角的设置（`Account Settings`）进入，然后点击菜单栏的 `SSH key` 进入页面添加 `SSH key`。  

点击 `Add SSH key` 按钮添加一个 `SSH key` 。把你复制的 `SSH key` 代码粘贴到 `key` 所对应的输入框中，记得 `SSH key` 代码的前后不要留有空格或者回车。  

当然，上面的 `Title` 所对应的输入框你也可以输入一个该 ` SSH key` 显示在 `github` 上的一个别名。  

默认的会使用你的邮件名称。

---

## 测试 SSH key

在 `git Bash` 中输入以下代码：  

	ssh -T git@github.com

当你输入以上代码时，会有一段警告代码，如：  

```shell
The authenticity of host 'github.com (207.97.227.239)' can't be established.
# RSA key fingerprint is 16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
# Are you sure you want to continue connecting (yes/no)?
```

【当第一次用`Git`的 `clone` 或者 `push` 命令连接`Github`时，会得到上面的警告，这是因为`Git`使用`SSH`连接，而`SSH`连接在第一次。  

验证`Github`服务器的`key`时，需要你确认`Github`的`Key`的指纹信息是否真的来自`Github`的服务器。  

这是正常的，输入 `yes` 回车既可。如果创建 `SSH key` 的时候设置了密码，接下来就会提示你输入密码，如：

```shell
Enter passphrase for key '/c/Users/Administrator/.ssh/id_rsa':
```

当然如果你密码输错了，会再要求你输入，直到对了为止。  

注意：输入密码时如果输错一个字就会不正确，使用删除键是无法更正的。  

密码正确后你会看到下面这段话，如：  

```shell
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

如果用户名是正确的,你已经成功设置`SSH`密钥。如果你看到` “access denied”` ，则表示拒绝访问，那么你就需要使用 `https` 去访问，而不是 `SSH` 。









