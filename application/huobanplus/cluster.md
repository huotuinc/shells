# 集群部署
## 所有机器互相信任
` firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="172.18.119.55" accept'
`

`firewall-cmd --reload
`
以及信任LB
sudo firewall-cmd --add-rich-rule='rule family="ipv4" source address="112.16.89.50" accept'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="10.25.87.146" accept'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" source address="172.18.255.139" accept'
sudo firewall-cmd --permanent --add-port=8003/tcp
sudo firewall-cmd --permanent --add-port=8009/tcp
sudo firewall-cmd --permanent --add-port=8015/tcp
sudo firewall-cmd --permanent --add-port=8021/tcp
sudo firewall-cmd --permanent --add-port=8027/tcp
sudo firewall-cmd --permanent --add-port=8033/tcp
sudo firewall-cmd --permanent --add-port=8039/tcp


所有服务器都互相hosts所有集群节点的名字


## 设定其中一台为中心服务器
c1.domain
是我们固定为它所取的名字
c1将负责处理我们的资源，以及维持JMS
其他节点的命名为
c1_n?.domain
### 安装activeMQ
./installActiveMQ.sh

还需要将相关的jar复制给tomcat

### 开放redis
sudo vim /etc/redis.conf
sudo systemctl restart redis
sudo systemctl status redis

### 开放资源访问用户
sudo systemctl stop tomcat_huotu
sudo usermod -s /bin/bash -d /home/huotu/home huotu
sudo mkdir /home/huotu/home
sudo chown huotu:huotu /home/huotu/home
sudo -u huotu ssh-keygen
sudo cat /home/huotu/home/.ssh/id_rsa.pub

##### 授权
sudo cat /home/huotu/home/.ssh/id_rsa.pub

sudo vim /home/huotu/home/.ssh/authorized_keys
sudo chown huotu:huotu /home/huotu/home/.ssh/authorized_keys
sudo chmod +r /home/huotu/home/.ssh/authorized_keys
##### 测试
sudo -u huotu sftp node1.d

## 使用支持集群的server和context


