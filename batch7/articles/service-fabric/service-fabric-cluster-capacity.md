<properties
   pageTitle="规划 Service Fabric 群集容量 | Azure"
   description="Service Fabric 群集容量规划注意事项。节点类型、持久性和可靠性层"
   services="service-fabric"
   documentationCenter=".net"
   authors="ChackDan"
   manager="timlt"
   editor=""/>  


<tags
   ms.service="service-fabric"
   ms.devlang="dotnet"
   ms.topic="article"
   ms.tgt_pltfrm="na"
   ms.workload="na"
   ms.date="09/09/2016"
   wacn.date="01/25/2017"
   ms.author="chackdan"/>  



# Service Fabric 群集容量规划注意事项

对于任何生产部署，容量规划都是一个重要的步骤。下面是在规划过程中必须注意的一些事项。

- 群集一开始需要的节点类型数目
- 每个节点类型的属性（大小、是否为主节点、是否面向 Internet、VM 数目，等等）
- 群集的可靠性和持久性特征

让我们简单地了解其中的每项。

## 群集一开始需要的节点类型数目

首先，你需要确定要创建的群集将用于什么目的，以及你打算要将哪些类型的应用程序部署到此群集中。如果你不清楚群集的用途，则很可能还未准备好进入容量规划流程。

确定群集一开始需要的节点类型数目。每个节点类型将映射到虚拟机规模集。然后，每个节点类型可以独立扩展或缩减、打开不同的端口集，并可以有不同的容量指标。因此，节点类型数目的确定基本上可归结为以下考虑因素：

- 应用程序是否有多个服务，其中是否有任何服务需是面向公众或面向 Internet 的服务？ 典型的应用程序包含可接收客户端输入的前端网关服务，以及一个或多个与前端服务通信的后端服务。因此，在此情况下，必须至少有两个节点类型。

- （构成应用程序）的服务是否有不同的基础结构要求，例如，更多的 RAM 或更高的 CPU 周期？ 例如，假设你要部署的应用程序包含前端服务和后端服务。前端服务可以在容量较小（D2 等的 VM 大小）且向 Internet 开放了端口的 VM 上运行。但是，后端服务计算密集型的服务，需要放在容量较大（D4、D6、D15 等的 VM 大小）且不连接到 Internet 的 VM 上运行。

 在本示例中，你可以决定将所有服务都放在一个节点类型上，但我们建议将它们分别放在群集中的两个节点类型上。这样，每个节点类型都有不同的属性，例如，Internet 连接或 VM 大小。也可以单独缩放 VM 的数目。

- 由于无法预见未来，因此，请利用所知道的事实，确定应用程序一开始需要的节点类型数目。以后，随时可以添加或删除节点类型。Service Fabric 群集必须至少有一个节点类型。

## 每个节点类型的属性

**节点类型**相当于云服务中的角色。节点类型定义 VM 大小、VM 数目及其属性。在 Service Fabric 群集中定义的每个节点类型将设置为不同的虚拟机规模集。VM 规模集是一种 Azure 计算资源，可用于将一组虚拟机作为一个集进行部署和管理。如果定义为不同的 VM 规模集，则每个节点类型可以独立扩展或缩减、打开不同的端口集，并可以有不同的容量指标。

群集可以有多个节点类型，但主节点类型（在门户定义的第一个节点类型）必须至少有 5 个 VM 供群集用于生产工作负荷（或至少有 3 个 VM 用于测试群集）。如果要使用 Resource Manager 模板创建群集，可以在节点类型定义下找到 **is Primary** 属性。主节点类型是 Service Fabric 系统服务所在的节点类型。

### 主节点类型
对于包含多个节点类型的群集，必须选择其中一个作为主节点类型。下面是主节点类型的特征：

- 主节点类型的 VM 大小下限取决于选择的持久性层。持久性层的默认值为 Bronze。有关持久性层的定义以及可采用的值的详细信息，请向下滚动。

- 主节点类型的 VM 数目下限取决于选择的可靠性层。可靠性层的默认值为 Silver。有关可靠性层的定义以及可采用的值的详细信息，请向下滚动。

- Service Fabric 系统服务（例如，群集管理器服务或映像存储服务）放在主节点类型上，因此，群集的可靠性和持久性取决于你为主节点类型选择的可靠性层值与持久性层值。

![显示具有两个节点类型的群集的屏幕截图][SystemServices]


### 非主节点类型
包含多个节点类型的群集有一个主节点类型，剩余的是非主节点类型。下面是非主节点类型的特征：

- 此节点类型的 VM 大小下限取决于选择的持久性层。持久性层的默认值为 Bronze。有关持久性层的定义以及可采用的值的详细信息，请向下滚动。

- 此节点类型的 VM 数目下限可以是 1。但是，你应该根据想要在此节点类型中运行的应用程序/服务的副本数目选择此数目。部署群集之后，节点类型中的 VM 数目可能会增加。


## 群集的持久性特征

持久性层用于向系统指示 VM 对于基本 Azure 基础结构拥有的权限。在主节点类型中，此权限可让 Service Fabric 暂停影响系统服务及有状态服务的仲裁要求的任何 VM 级别基础结构请求（例如，VM 重新启动、VM 重置映像或 VM 迁移）。在非主节点类型中，此权限可让 Service Fabric 暂停影响其中运行的有状态服务的仲裁要求的任何 VM 级别基础结构请求，例如，VM 重新启动、VM 重置映像、VM 迁移，等等。

此权限表示为以下值：

- Gold - 每个 UD 可持续暂停基础结构作业 2 小时

- Silver - 每个 UD 可持续暂停基础结构作业 30 分钟（当前未启用。启用后，将在所有单核及更高配置的标准 VM 上提供此功能）。

- Bronze - 无权限。这是默认值。

## 群集的可靠性特征

可靠性层用于设置你想要在此群集中的主节点类型上运行的系统服务副本数。副本数越大，群集中的系统服务越可靠。

可靠性层可以采用以下值。

- Platinum - 运行包含 9 个目标副本集的系统服务

- Gold - 运行包含 7 个目标副本集的系统服务

- Silver - 运行包含 5 个目标副本集的系统服务

- Bronze - 运行包含 3 个目标副本集的系统服务

>[AZURE.NOTE] 选择的可靠性层决定了主节点类型必须具有的节点数下限。可靠性层与群集大小上限没有关系。因此，你可以在 Bronze 可靠性层运行包含 20 个节点的群集。

 随时可以选择将群集的可靠性从一个层更新为另一个层。这样做会触发更改系统服务副本集计数所需的群集升级。等待升级完成，然后对群集做出其他任何更改，如添加节点，等等。可以在 Service Fabric Explorer 中运行 [Get-ServiceFabricClusterUpgrade](https://msdn.microsoft.com/zh-cn/library/mt126012.aspx) 来监视升级进度

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## 后续步骤

完成容量规划并设置群集后，请阅读以下文章：

- [Service Fabric 群集安全性](/documentation/articles/service-fabric-cluster-security/)
- [Service Fabric 运行状况模型简介](/documentation/articles/service-fabric-health-introduction/)

<!--Image references-->

[SystemServices]: ./media/service-fabric-cluster-capacity/SystemServices.png

<!---HONumber=Mooncake_Quality_Review_0125_2017-->