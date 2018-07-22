# 本地git仓库与github仓库交互

#### 创建ssh

本地git仓库和github之间是通过ssh加密的，所以首次在一台计算机上使用github时需要创建ssh密钥，可以按照如下步骤：

1. gitbash中输入 
> ssh-keygen -t rsa -C " youremail@example.com"

注意：
* <i>"-C" 大写</i>
* 引号部分替换为自己的邮箱

通过这条命令在本地计算机创建了一个.ssh文件夹，可以在用户主目录下找到这个文件夹，打开这个文件夹，可以发现两个文件，分别是id_rsa和id_rsa.pub，第一个文件是加密用的私钥，第二个文件是公钥

2. 登录github，进入settings>SSH and GPG keys>NEW SSH key，Title可以随便填写，将刚才第一步生成的公钥文件id_rsa.pub文件中的内容复制到key文本框中，点击add ssh key

#### 与github建立连接

1.在 