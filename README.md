# -Centos7-ssh-
修改Centos7远程ssh登陆端口,并在防火墙里开通修改的端口可用于登陆

原文地址:https://www.cmsky.com/centos7-ssh-port/

centos7修改ssh默认登录端口和centos6差不多，就是防火墙不一样，然后关闭selinux最好。

修改ssh默认22端口
vi /etc/ssh/sshd_config

在Port 22下面加一行，以端口50000为例，Port 50000

然后保存，重启ssh服务systemctl restart sshd.service

防火墙中放行新加入端口
firewall-cmd --permanent --add-port=50000/tcp

用该命令查询firewall-cmd --permanent --query-port=50000/tcp
如果是yes就是添加成功，如果是no就是没成功

成功后重载防火墙firewall-cmd --reload

关闭selinux
查看selinux状态sestatus，如果是enabled就是开启状态

vi /etc/selinux/config

修改SELINUX=disabled

然后重启vps试试用新的50000端口登录，如果登录成功再vi /etc/ssh/sshd_config把Port 22端口删除，再重启ssh服务就好了。


