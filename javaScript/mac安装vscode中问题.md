### git提交错误
1. `ssh -T git@gitee.com`
输入命令：`ssh -T git@gitee.com ` 再输入yes之后 再重复输入此条命令
首次解决网址：https://blog.csdn.net/weixin_42284867/article/details/90730560
### git clone错误
* `warning: templates not found in /usr/local/git/share/git-core/templates`
解决方法：
在终端输入以下指令：
sudo mkdir /usr/local/git 确保上级目录存在，不然就 sudo mkdir -p /usr/local/git
sudo mkdir /usr/local/git/share
sudo mkdir /usr/local/git/share/git-core
sudo mkdir /usr/local/git/share/git-core/templates
sudo chmod -R 755 /usr/local/git/share/git-core/templates
在第一条指令输入后，需要输入此Mac的密码。最后重新克隆即可。


