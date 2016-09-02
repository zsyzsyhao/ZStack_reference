# 概述

## 文档目的

本文档主要介绍Mevoco的各个资源以及每个资源状态变化的条件。用户可以在文档中找到Mevoco中所有功能的底层逻辑，从而对每个资源的操作有清楚的认识。此外，在使用Mevoco的过程中出现问题时，能根据本文档中的线索找到问题的源头和解决方案。 

产品手册里会详细介绍Mevoco的各个资源的操作、使用场景和错误处理。

每个资源作为一章节，每个章节还会划分为以下几个部分：

简介：简单介绍一下该功能的背景。

状态：

操作：

清单（Inventory）: 介绍该功能各种资源(例如主机区域（zone）, 虚拟机（virtual machine）)的清单，也就是在使用各种Query API得到的返回结果。 

我们会使用表格来展示清单，表格的左边是资源的名字，右侧会介绍该资源的用途。操作: 介绍和该功能有关的API操作。

我们还将结合ZStack的命令行工具`zstack-cli`来介绍每个API的使用方法。

全局配置（Global Configurations）: 介绍和该功能有关的全局配置参数。

系统标签（System Tags）: 介绍和该功能有关的系统标签。我们推荐用户从:ref:Introduction`开始，然后至少阅读:ref:`Resource Model <resource>, Command LineTool, 和:ref:Query <query> 。

这些将会对日常使用ZStack非常关键。对于其他章节，你可以按需阅读。 例如，当你需要创建虚拟机的时候，再来阅读 Virtual Machine 。 


## 读者对象

本文档详述了Mevoco云系统部署的安装、使用教程。本文档主要适用于以下读者：

* 技术支持工程师
* 部署运维工程师
* 产品咨询工程师
* 对Mevoco有兴趣研究的相关人员

## 名词解释

| 术语 | 概念 |
| --- | --- |
| 区域 | 安装Mevoco系统的物理主机，提供UI管理、云系统部署功能 |
| 集群 | 一个集群是类似主机（Host）组成的逻辑组. 在同一个集群中的主机必须安装相同的操作系统（虚拟机管理程序,hypervisor）, 拥有相同的二层网络连接, 可以访问相同的主存储. 在实际的数据中心, 一个集群通常对应一个机架（rack） |
| 物理机 | 也称之为物理机，为云主机实例提供计算、内存、网络、存储的物理主机。虽然可以添加管理节点为一个计算节点，但不建议在生产环境中这么部署 |
| 云主机 | Mevoco 特制虚拟机，即运行在物理机上的虚拟机实例，具有独立的IP地址，可以安装部署应用服务 |
| 主存储 | 用于存储云主机的磁盘文件的存储服务器。支持本地存储、NFS、Ceph、Fusionstor、Shared Mount Point等类型 |
| 镜像 | 云主机所使用的镜像模板文件，包含了云主机的操作系统，也可以定制安装相应的软件 |
| 镜像服务器 | 也称之为备份存储服务器，存储云主机镜像文件的物理主机。建议单独部署镜像服务器 |
| 镜像仓库 | 可以为正在运行的云主机快速创建镜像，可以高效的管理虚拟机镜像的版本变迁以及发布，实现快速上传、下载镜像，镜像快照，以及导出镜像的操作。 |
| 云盘 | 云主机的数据盘，给云主机提供额外的存储空间，一块云盘在同一时刻只能挂载到一个云主机。一个云主机最多可以挂载24块云盘 |
| 计算规格 | 启动云主机涉及到的CPU数量、内存、网络设置等规格定义 |
| 云盘规格 | 创建云盘容量大小的规格定义 |
| 安全组 | 针对云主机进行第三层网络的防火墙控制，对IP地址、网络包类型或网络包流向等可以设置不同的安全规则 |
| L2NoVlanNetwork | 物理主机的网络连接不采用Vlan设置 |
| L2VlanNetwork | 物理主机节点的网络连接采用Vlan设置，Vlan需要在交换机端提前进行设置 |
| 二层网络 | 计算节点的物理网卡设备名称，例如eth0 |
| 三层网络 | 云主机使用的网络配置，包括IP地址范围，网关，DNS等 |
| 公有网络 | 由因特网信息中心分配的公有IP地址或者可以连接到外部互联网的IP地址 |
| 私有网络 | 云主机连接和使用的内部网络 |
| 弹性IP | 公有网络接入到私有网络的IP地址 |


