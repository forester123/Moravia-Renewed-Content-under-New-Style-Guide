<properties 
	pageTitle="部署业务线应用程序 | Microsoft Azure" 
	description="在 Azure 中通过 SQL Server AlwaysOn 可用性组分五个阶段部署基于 Web 的高可用性业务线应用程序。" 
	documentationCenter=""
	services="virtual-machines" 
	authors="JoeDavies-MSFT" 
	manager="timlt" 
	editor=""
	tags="azure-resource-manager"/>  


<tags 
	ms.service="virtual-machines" 
	ms.date="12/17/2015" 
	wacn.date=""/>

# 在 Azure 中部署高可用性业务线应用程序

[AZURE.INCLUDE [learn-about-deployment-models](../includes/learn-about-deployment-models-rm-include.md)] 经典部署模型。

本主题包含有关在 Azure 基础结构服务中通过 SQL Server AlwaysOn 可用性组部署仅限 Intranet 的基于 Web 的高可用性业务线应用程序的分步说明链接。在以下计算机上托管应用程序：

- 两个 Web 服务器
- 两个数据库服务器
- 一个群集多数节点服务器
- 两个域控制器

这是包含每个服务器的占位符名称的配置。

![](./media/virtual-machines-workload-high-availability-LOB-application-overview/workload-lobapp-phase4.png)
 
至少为每个角色配置两台计算机可确保高可用性。所有虚拟机都位于一个 Azure 位置（也称为区域）。用于特定角色的每个虚拟机组在其自己的可用性集中。

## 材料清单

此基线配置需要以下一组 Azure 服务和组件：

- 七个虚拟机
- 四个用于域控制器和运行 SQL Server 的虚拟机的额外数据磁盘
- 三个可用性集
- 一个跨界虚拟网络
- 两个存储帐户

下面是此配置的虚拟机及其默认大小。

项目 | 虚拟机说明 | 库映像 | 默认大小 
--- | --- | --- | --- 
1\. | 第一个域控制器 | Windows Server 2012 R2 Datacenter | D1
2\. | 第二个域控制器 | Windows Server 2012 R2 Datacenter | D1
3\. | 主数据库服务器 | Microsoft SQL Server 2014 Enterprise - Windows Server 2012 R2 | D4
4\. | 辅助数据库服务器 | Microsoft SQL Server 2014 Enterprise - Windows Server 2012 R2 | D4
5\. | 群集多数节点 | Windows Server 2012 R2 Datacenter | D1
6\. | 第一个 Web 服务器 | Windows Server 2012 R2 Datacenter | D3
7\. | 第二个 Web 服务器 | Windows Server 2012 R2 Datacenter | D3

若要计算此配置的估计成本，请参阅 [Azure 定价计算器](https://azure.microsoft.com/pricing/calculator/)。

1. 在“模块”中，单击“计算”，然后单击“虚拟机”足够多的次数，以创建包含七个虚拟机的列表。
2. 对于每个虚拟机，请选择：
	- 所需的区域
	- 对于类型，选择 **Windows**
	- 对于定价层，选择“标准”
	- 上一个表中的默认大小，或者在**实例大小**中选择所需的大小

> [AZURE.NOTE] Azure 定价计算器不包括运行 SQL Server 2014 Enterprise 的两个虚拟机的额外 SQL Server 许可证成本。有关详细信息，请参阅[虚拟机定价-SQL](https://azure.microsoft.com/pricing/details/virtual-machines/#Sql)。

## 部署阶段

此配置的部署分为以下几个阶段：

- [阶段 1：配置 Azure](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase1)。创建存储帐户、可用性集和跨界虚拟网络。
- [阶段 2：配置域控制器](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase2)。创建和配置副本 Active Directory 域服务 (AD DS) 域控制器。
- [阶段 3：配置 SQL Server 基础结构](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase3)。创建并配置运行 SQL Server 的虚拟机，创建群集并启用 SQL Server AlwaysOn 可用性组。
- [阶段 4：配置 Web 服务器](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase4)。创建并配置两个 Web 服务器虚拟机。
- [阶段 5：将应用程序数据库添加到 SQL Server AlwaysOn 可用性组](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase5)。准备业务线应用程序数据库并将它们添加到 SQL Server AlwaysOn 可用性组。

此部署旨在补充[业务线应用程序体系结构蓝图](http://msdn.microsoft.com/dn630664)并引入最新建议。

这是一种预定义的规范性体系结构。请记住以下几点：

- 如果你是一名经验丰富的基于 Web 的业务线应用程序实施者，请随意调整阶段 3 到阶段 5 中的说明并生成最适合你的需求的应用程序基础结构。 
- 如果你已有现有 Azure 混合云实施，请随意调整或跳过阶段 1 和阶段 2 中的说明，以在相应子网上托管新应用程序的虚拟机。
- 所有服务器都位于 Azure 虚拟网络中的单个子网上。如果要提供等效于子网隔离的附加安全性，则可以使用[网络安全组](../virtual-networks/virtual-networks-nsg.md)。

若要构建此配置的开发/测试环境或概念证明，请参阅[在混合云中设置基于 Web 的 LOB 应用程序用于测试](../virtual-network/virtual-networks-setup-lobapp-hybrid-cloud-testing.md)。

有关针对 Azure 设计 IT 工作负荷的其他信息，请参阅 [Azure 基础结构服务实施准则](/documentation/articles/virtual-machines-infrastructure-services-implementation-guidelines)。

## 后续步骤

若要开始配置此工作负荷，请转到[阶段 1：配置 Azure](/documentation/articles/virtual-machines-workload-high-availability-LOB-application-phase1)。

<!---HONumber=Mooncake_Quality_Review_1215_2016-->