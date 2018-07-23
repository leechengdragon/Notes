# 本地git仓库与github仓库交互

#### 创建ssh

本地git仓库和github之间是通过ssh加密的，所以首次在一台计算机上使用github时需要创建ssh密钥，可以按照如下步骤：

1. gitbash中输入 
> ssh-keygen -t rsa -C " youremail@example.com"

<i>注意：</i>
* "-C" 大写
* 引号部分替换为自己的邮箱

通过这条命令在本地计算机创建了一个.ssh文件夹，可以在用户主目录下找到这个文件夹，打开这个文件夹，可以发现两个文件，分别是id_rsa和id_rsa.pub，第一个文件是加密用的私钥，第二个文件是公钥

2. 登录github，进入settings>SSH and GPG keys>NEW SSH key，Title可以随便填写，将刚才第一步生成的公钥文件id_rsa.pub文件中的内容复制到key文本框中，点击add ssh key

#### 与github建立连接

假设在github中建立了一个名叫Test的库，现在需要将本地库与该库连接并同步

1.gitbash中输入

>git remote add origin git@github.com:yourgithubusername/Test.git

或者

>git remote add origin https://github.com/yourgithubusername/Test.git

第一种方式使用ssh协议，第二中方式使用http协议，推荐使用第一种方式，第二种方式每次提交时都会输入用户名和密码，很不方便

2.推送代码

>git push -u origin master

3.获取代码

>