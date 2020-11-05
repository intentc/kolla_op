#!/usr/bin/env bash
#setenforce 0
#hostnamectl set-hostname openstack91
sed -i  "s#SELINUX=enforcing#SELINUX=disabled#g"  /etc/sysconfig/selinux
systemctl disable firewalld --now;
cat <<-EOF >> /etc/hosts
10.16.140.91   openstack91
10.16.140.92   openstack92
10.16.140.93   openstack93
10.16.140.32   openstack32
EOF
sleep 1；

rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-7
sudo yum clean all
sudo yum makecache fast
yum -y install epel-release
yum -y install python-pip
#https://blog.csdn.net/qq_15098623/article/details/90905230
mkdir ~/.pip
cat << EOF > ~/.pip/pip.conf
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple/
[install]
trusted-host=pypi.tuna.tsinghua.edu.cn
EOF
sleep 1；

sudo yum -y install git screen lrzsz wget sshpass tree
sudo yum install python-devel libffi-devel gcc openssl-devel libselinux-python -y
sleep 1；

wget -P /etc/yum.repos.d/ https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
sudo yum -y install  docker-ce-19.03.6-3.el7
sudo systemctl enable docker --now
sudo yum install -y python2-docker
#或pip install docker
sleep 1；

sed -i "s#\[Service\]#\[Service\]\nMountFlags=shared#g" /usr/lib/systemd/system/docker.service
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://q9v6f7q7.mirror.aliyuncs.com"],
  "max-concurrent-downloads": 10
}
EOF
systemctl daemon-reload
systemctl restart docker
