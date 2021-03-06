<properties
	pageTitle="Azure 虚拟机中的 SQL Server 概述 | Azure"
	description="了解如何在 Azure 虚拟机上运行完整的 SQL Server 版本。获取所有 SQL Server VM 映像和相关内容的直接链接。"
	services="virtual-machines-windows"
	documentationCenter=""
	authors="rothja"
	manager="jhubbard"
	editor=""
	tags="azure-service-management"/>  


<tags
	ms.service="virtual-machines-windows"
	ms.devlang="na"
	ms.topic="get-started-article"
	ms.tgt_pltfrm="vm-windows-sql-server"
	ms.workload="infrastructure-services"
	ms.date="10/11/2016"
	wacn.date=""
	ms.author="jroth"/>  


# Azure 虚拟机中的 SQL Server 概述

本主题介绍了在 Azure 虚拟机 (VM) 上运行 SQL Server 的选项，提供了[门户映像链接](#option-1-create-a-sql-vm-with-per-minute-licensing)，同时概述了[常见任务](#manage-your-sql-vm)。

>[AZURE.NOTE] 如果用户已熟悉 SQL Server，只是想了解如何部署 SQL Server VM，则请参阅[在 Azure 门户预览中预配 SQL Server 虚拟机](/documentation/articles/virtual-machines-windows-portal-sql-server-provision/)。

## 概述
如果是数据库管理员或开发人员，Azure 虚拟机能够将本地 SQL Server 工作负荷和应用程序迁移到云。下面的视频是关于 SQL Server Azure VM 的技术概述。

## 了解你的选项
选择用在 Azure 中托管数据有诸多理由。将应用程序移到 Azure 后，移动数据的性能也有改善。而且还有其他方面的好处。会自动获取多个数据中心的访问权限，从而获得全局支持和灾难恢复能力。并且数据持久保存、高度安全。

可用使用“在 Azure VM 中运行 SQL Server”选项在 Azure 中存储关系数据。下表是 Azure 上 SQL 产品的快速摘要。

|&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| SQL 产品 | 说明 |
|---:|---|---|
|![Azure 虚拟机中的 SQL Server](./media/virtual-machines-windows-sql-server-iaas-overview/sql-server-virtual-machine.png)  
|[Azure 虚拟机中的 SQL Server](/home/features/virtual-machines/#home_vm_overview_info)|在 Azure 虚拟机中运行 SQL Server（本主题重点）。在零售版 SQL Server 上直接管理虚拟机并运行数据库。 |
|![SQL 数据库](./media/virtual-machines-windows-sql-server-iaas-overview/azure-sql-database.png)  
|[SQL 数据库](/home/features/sql-database/)|使用 SQL 数据库服务来访问和缩放数据库，而无需管理底层基础结构。|
|![SQL 数据仓库](./media/virtual-machines-windows-sql-server-iaas-overview/azure-sql-data-warehouse.png)  
|[SQL 数据仓库](https://azure.microsoft.com/services/sql-data-warehouse/)|使用 Azure SQL 数据仓库来处理大量的关系与非关系数据。以服务形式提供可缩放的数据仓库功能。|
|![SQL Server Stretch Database](./media/virtual-machines-windows-sql-server-iaas-overview/sql-server-stretch-database.png)  
|[SQL Server Stretch Database](https://azure.microsoft.com/services/sql-server-stretch-database/)|将本地事务数据从 Microsoft SQL Server 2016 动态延伸到 Azure。|

使用这些不同的选项，运行于 Azure VM 上的 SQL Server 可以很好地应用于多种场景。例如，你可能想要配置与本地 SQL Server 计算机高度相似的 Azure VM。或者可能想要在同一数据库服务器上运行其他应用程序和服务。有两个资源，可帮助你详细思考决策因素：

 - [Azure 虚拟机上的 SQL Server](/home/features/virtual-machines/#home_vm_overview_info) 概述了在 Azure VM 上使用 SQL Server 的最佳方案。
 - [选择云 SQL Server 选项：Azure SQL (PaaS) 数据库或 Azure VM 上的 SQL Server (IaaS)](/documentation/articles/sql-database-paas-vs-sql-server-iaas/) 介绍了 SQL 数据库与运行于 VM 上的 SQL Server 之间的详细比较。

## 创建新的 SQL VM
以下部分提供了直接链接，可链接到 Azure 门户预览的 SQL Server 虚拟机库映像。

有关教程中此过程的分步指导，请参阅[在 Azure 门户预览中预配 SQL Server 虚拟机](/documentation/articles/virtual-machines-windows-portal-sql-server-provision/)。另请查看 [Performance best practices for SQL Server VMs](/documentation/articles/virtual-machines-windows-sql-performance/)（SQL Server VM 的性能最佳实践），该文介绍了如何在预配期间选择适当的虚拟机大小和其他可用功能。

## <a name="option-1-create-a-sql-vm-with-per-minute-licensing"></a> 选项 1：使用每分钟许可创建 SQL VM
下表提供了虚拟机库中提供的 SQL Server 映像的矩阵。单击任何链接，即可开始创建具有指定版本和操作系统的新 SQL VM。

|版本|操作系统|版本|
|---|---|---|
|**SQL 2016**|Windows Server 2012 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2016RTMStandardWindowsServer2012R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2016RTMWebWindowsServer2012R2)、[Dev](https://portal.azure.cn/#create/Microsoft.SQLServer2016RTMDeveloperWindowsServer2012R2)、[Express](https://portal.azure.cn/#create/Microsoft.SQLServer2016RTMExpressWindowsServer2012R2)|
|**SQL 2014 SP1**|Windows Server 2012 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP1EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP1StandardWindowsServer2012R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP1WebWindowsServer2012R2)、[Express](https://portal.azure.cn/#create/Microsoft.SQLServer2014SP1ExpressWindowsServer2012R2)|
|**SQL 2014**|Windows Server 2012 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2014EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2014StandardWindowsServer2012R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2014WebWindowsServer2012R2)|
|**SQL 2012 SP3**|Windows Server 2012 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3StandardWindowsServer2012R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3WebWindowsServer2012R2)、[Express](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP3ExpressWindowsServer2012R2)|
|**SQL 2012 SP2**|Windows Server 2012 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012R2)|
|**SQL 2012 SP2**|Windows Server 2012|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2EnterpriseWindowsServer2012)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2StandardWindowsServer2012)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2WebWindowsServer2012)、[Express](https://portal.azure.cn/#create/Microsoft.SQLServer2012SP2ExpressWindowsServer2012)|
|**SQL 2008 R2 SP3**|Windows Server 2008 R2|[Enterprise](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3EnterpriseWindowsServer2008R2)、[Standard](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3StandardWindowsServer2008R2)、[Web](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3WebWindowsServer2008R2)|
|**SQL 2008 R2 SP3**|Windows Server 2012|[Express](https://portal.azure.cn/#create/Microsoft.SQLServer2008R2SP3ExpressWindowsServer2012)|

## <a name="manage-your-sql-vm"></a> 管理 SQL VM
预配 SQL Server VM 之后，有几项可选的管理任务。在许多方面，完全可以像管理本地 SQL Server 实例一样配置和管理 SQL Server。但某些任务是特定于 Azure 的。下列各节重点介绍上述某些领域并提供详细信息链接。

### 连接到 VM
其中一个最基本的管理步骤是，通过工具连接到 SQL Server VM，如 SQL Server Management Studio (SSMS)。有关如何连接到新 SQL Server VM 的说明，请参阅[连接到 Azure 上的 SQL Server 虚拟机](/documentation/articles/virtual-machines-windows-sql-connect/)。

### 迁移数据
如果已有数据库，你会想要将该数据库移至新预配的 SQL VM。有关迁移选项的列表和指导，请参阅 [Migrating a Database to SQL Server on an Azure VM](/documentation/articles/virtual-machines-windows-migrate-sql/)（将数据库迁移到 Azure VM 上的 SQL Server）。

### 配置高可用性
如果你需要高可用性，请考虑配置 SQL Server 可用性组。这涉及虚拟网络中的多个 Azure VM。Azure 门户预览有一个模板，为用户设置了此配置。有关详细信息，请参阅[在 Azure Resource Manager 虚拟机中配置 AlwaysOn 可用性组](/documentation/articles/virtual-machines-windows-portal-sql-alwayson-availability-groups/)。如果想要手动配置可用性组和关联的侦听器，请参阅[在 Azure VM 中配置 AlwaysOn 可用性组](/documentation/articles/virtual-machines-windows-portal-sql-alwayson-availability-groups-manual/)。

有关其他高可用性注意事项，请参阅 [Azure 虚拟机中 SQL Server 的高可用性和灾难恢复](/documentation/articles/virtual-machines-windows-sql-high-availability-dr/)。

### 备份数据
Azure VM 可以利用[自动备份](/documentation/articles/virtual-machines-windows-sql-automated-backup/)，定期创建数据库到 Blob 存储的备份。你也可以手动使用此技术。有关详细信息，请参阅 [Use Azure Storage for SQL Server Backup and Restore](/documentation/articles/virtual-machines-windows-use-storage-sql-server-backup-restore/)（使用 Azure 存储进行 SQL Server 备份和还原）。有关所有备份和还原选项的概述，请参阅 [Backup and Restore for SQL Server in Azure Virtual Machines](/documentation/articles/virtual-machines-windows-sql-backup-recovery/)（Azure 虚拟机中 SQL Server 的备份和还原）。

### 自动更新
Azure VM 可以使用[自动修补](/documentation/articles/virtual-machines-windows-sql-automated-patching/)来安排维护时段，以便自动安装重要的 Windows 和 SQL Server 更新。

### 客户体验改善计划 (CEIP)
客户体验改善计划 (CEIP) 默认情况下已启用。它定期将报表发送给 Microsoft，以帮助改进 SQL Server。CEIP 不要求管理任务，除非想在预配后禁用它。你可以通过远程桌面连接到 VM，以自定义或禁用 CEIP。然后运行 **SQL Server 错误和使用情况报告**实用工具。请按照说明禁用报告功能。

有关详细信息，请参阅[接受许可条款](https://msdn.microsoft.com/zh-cn/library/ms143343.aspx)主题的 CEIP 部分。

## 后续步骤

其他问题？ 请先参阅 [Azure 虚拟机中的 SQL Server 常见问题解答](/documentation/articles/virtual-machines-windows-sql-server-iaas-faq/)。同时将问题或看法添加到任何 SQL VM 主题的底部，以便与 Azure.cn 和社区互动。

<!---HONumber=Mooncake_Quality_Review_1202_2016-->