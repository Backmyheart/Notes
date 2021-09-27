# VIM

## vim命令记录

### vim 打开多个文件

vim打开多个文件、同时显示多个文件、在文件之间切换：  

* vim还没启动的时候：  

>	vim file1 file2 …… filen

* vim已经启动：  

>	在命令行状态下输入	:open file
>	可以在打开一个文件，并且此时vim里会显示出file文件的内容







---

## Vundle 插件管理器

### 背景  

Vim缺乏默认的插件管理器，所有插件的文件都散布在 `~/.vim` 下的几个文件夹中，插件的安装、更新和删除都需要自己手动来，既麻烦费事，又可能出现错误。  

### Vundle简介  

Vundle 是 Vim bundle 的简称，是一个Vim插件管理器。  

只需要在 `.vimrc` 添加上控件名，Vundle 可以帮我们下载到插件文件夹：`/Users/{username}/.vim/bundle`  

### Vundle安装

>	git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim  

### 配置说明

插件有三种类型：  

* Github 上 vim-scripts 仓库的插件  
* Github 上 非vim-scripts 仓库的插件  
* 不在 Github 上的插件  

对于不同的插件，Vundle 自动管理和下载插件的时候，有不同的地址填写方法，有如下三类：  

* 在 Github 上 vim-scripts 用户下的仓库，只需写出 repos（仓库）名称  
* 在 Github 其它用户下的 repos，需要写出 “用户名/repos名”  
* 不在 Github 上的插件，需写出 git 全路径  

### Vundle配置插件

在终端通过 vim 打开 `~/.vimrc` 文件：  

>	vim ~/.vimrc  

将以下内容加在 `.vimrc` 文件中，加入保存之后，就可以使用Vundle了：  

```shell
filetype off						" 必须要添加

" 设置包括vundle和初始化相关的runtime path
set rtp+=~/.vim/bundle/Vundle.vim

" 请将安装插件的命令放在 vundle#begin 和 vundle#end 之间
call vundle#begin()

" 让vundle管理插件版本，必须
Plugin 'VundleVim/Vundle.vim'


" 以下范例用来支持不同格式的插件安装

" Github上 vim-scripts 仓库的插件（http://vim-scripts.org/vim/scripts.html）
" Plugin '插件名称'     实际上是 Plugin 'vim-scripts/插件仓库名'，只是此处的用户名可以省略
Plugin 'L9'


" Github上 非vim-scripts 仓库的插件
" 格式为	Plugin '用户名/插件仓库名'
Plugin 'tpope/vim-fugitive'


" 由Git支持，但不在 Github 上的插件仓库
" 格式为	Plugin 'git clone 仓库地址'
Plugin 'git://git.wincent.com/command-t.git'


" 本地的Git仓库（例如自己写的插件）
" 格式为	Plugin 'file:///本地插件仓库的绝对路径'
Plugin 'file:///home/kylin/path/to/plugin'


" 你所有的插件需要在下面这行之前
call vundle#end()				" Required


filetype plugin indent on		" 加载 vim自带 和 插件相应的语法和文件类型相关脚本
filetype plugin on				" 忽视插件改变缩进
```

**注意：以后安装新插件就直接编辑`vimrc`，添加`plugin`就行了，在这里添加的`plugin`只是例子，你可以不安装这些插件，换上自己需要安装的插件。**  

### Vundle常用的命令

* 常用的命令：  

```shell
PluginList			# 列出所有已配置的插件
PluginInstall		# 安装插件，追加 ‘!’ 用以更新
PluginUpdate		# 更新插件
PluginSearch foo	# 搜索foo；追加 ‘!’ 清除本地缓存
PluginClean			# 清除未使用插件，需要确认；追加 ‘!’ 自动批准移除未使用插件
```

* 插件安装：  

1. 将想要安装的插件，按照地址填写方法，将地址填写在vundle#begin和vundle#end之间就可以。  

2. 保存之后，有两种方法安装插件。  

（1）运行 `vim`，再运行 `:PluginInstall`  

（2） 通过命令行直接安装 `vim +PluginInstall +qall`  

* 移除不需要的插件：  

1. 编辑 `.vimrc` 文件移，移除插件所对应的 `plugin` 那一行。  

2. 保存退出当前的`vim`。  

3. 重新打开`vim`，输入命令`BundleClean`。  

参考链接：https://blog.csdn.net/weixin_30477293/article/details/99259054  



---

## ctags的安装和使用

### 安装

```Shell
sudo apt-cache search ctags
sudo apt-get install exuberant-ctags
```

### ctags -R

执行命令 `ctags -R` 或 `ctags -R *`生成索引文件，“-R” 表示递归创建，也就包括源代码根目录下的所有子目录下的源程序。  

### 跳转方法（配置）

vim 用这个 `tags` 文件来定位做了标记的对象。定位这些对象的方法：  

1. 用`vim`打开某个源代码文件后，在命令行模式设置`tags`源，`:set tags=`命令来设定`tags`文件的路径，这样`vim`才能找到`tags`文件。例如：`:set tags=/home/kylin/xxx/tags`。【不需要在`tags`文件所在的目录】  

2. 在`tags`文件所在的目录下，在运行`vim`的时候加上`-t` 参数，例如：`vim -t foo_bar`，这个命令将打开定义`foo_bar`（变量或函数或其它）的文件，并把光标定位到这一行。  

3. 在`tags`文件所在的目录下，在`vim`编辑器的命令行模式用 `:ta` 命令，例如：`:ta foo_bar`，跳转到函数`foo_bar`定义处。  

4. 通用方法（**推荐**）：编辑`vimrc`文件，加上如下语句：  

```shell
set tags=tags;		" 注意分号 ; 不可省略，表示若当前目录中不存在tags， 则在父目录中寻找，一直向上递归
set autochdir		" 在vim中编辑多个文件，并在它们之间切换时（因为要不断跳转），有个问题是：工作目录通常是你打开第一个文件的那个目录。所以，将工作目录自动切换到正在编辑的文件所在的目录是很有用的。需要启用该选项。
```


关于ctags的更多使用方法，可参考链接：https://www.cnblogs.com/cdwodm/archive/2012/11/01/2750233.html  



