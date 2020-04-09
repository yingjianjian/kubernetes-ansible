# kubernets-ansible

**基于ansible实现kubernetes集群部署**
>ansible-playbook (2.9.6)

>部署集群类型：二进制kubernetes v17.3 + haproxy + keepalived + etcd+bootstrap自动签署

## 使用方法
    
    将二进制包放到指定目录kubernetes-server-linux-amd64.tar.gz 和 kubernetes-node-linux-amd64.tar.gz 放到master 和 node 以及addnode的files目录下

    修改hosts文件根据不同组放入不同的主机ip，格式：主机名 ansible_ssh_host=ip地址 ansible_connection=ssh ansible_ssh_user=root ansible_ssh_pass=yingjianjian

    带有cfsssl=true代表master-1的主机 主要用来生成各类证书 已经kubectl的操作

    执行一键安装命令： `ansible-playbook kubernetes.yml`

    执行init以及docker的时候有许多安装基础组件的功能类似于docker的安装 此过程因网络问题可能会出现报错 重复执行即可

## 目录结构解析

+ roles
   + init：   初始化系统模块
   + docker： 安装docker部署
   + etd：  安装etcd集群
   + haproxy： 安装haproxy
   + keepalived： 安装keepalived
   + master：安装kube-apiserver,kube-controller-manager,kube-scheduler
   + node: 安装kube-proxy kubelet
   + addods: 安装kube-dns
   + addnode: 第一次部署集群不需要执行  后续新增节点需要单独执行这个模块
+ group_vars:  群组变量  kubernetes 里的所有变量都在这个目录里定义
+ hosts: 主机inventory  定义不同主机组对应不同roles
