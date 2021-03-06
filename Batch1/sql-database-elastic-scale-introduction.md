<properties
    pageTitle="扩展 Azure SQL 数据库 | Azure"
    description="软件即服务 (SaaS) 开发人员可以使用这些工具轻松地在云中创建可缩放的弹性数据库"
    services="sql-database"
    documentationCenter=""
    manager="jhubbard"
    authors="ddove"
    editor=""/>  


<tags
    ms.service="sql-database"
    ms.workload="sql-database"
    ms.tgt_pltfrm="na"
    ms.devlang="na"
    ms.topic="article"
    ms.date="09/06/2016"
    ms.author="ddove"/>  


# 扩展 Azure SQL 数据库

可以使用**弹性数据库**工具轻松地扩展 Azure SQL 数据库。借助这些工具和功能，可以使用 **Azure SQL 数据库**中几乎不受限制的数据库资源来为事务工作负荷，尤其是软件即服务 (SaaS) 应用程序创建解决方案。弹性数据库的功能包括：

* [弹性数据库客户端库](/documentation/articles/sql-database-elastic-database-client-library/)：客户端库是一项功能，可用于创建和维护分片数据库。请参阅[弹性数据库工具入门](/documentation/articles/sql-database-elastic-scale-get-started/)。
* [弹性数据库拆分/合并工具](/documentation/articles/sql-database-elastic-scale-overview-split-and-merge/)：在分片数据库之间移动数据。这对于将数据从多租户数据库移动到单租户数据库很有用（反之亦然）。请参阅[弹性数据库拆分/合并工具教程](/documentation/articles/sql-database-elastic-scale-configure-deploy-split-and-merge/)。
* [弹性数据库作业](/documentation/articles/sql-database-elastic-jobs-overview/)（预览版）：使用作业来管理大量的 Azure SQL 数据库。轻松执行管理操作，例如，使用作业更改架构、管理凭据、更新引用数据、收集性能数据，或收集租户（客户）遥测数据。
* [弹性数据库查询](/documentation/articles/sql-database-elastic-query-overview/)（预览版）：可跨多个数据库运行 Transact-SQL 查询。这样，便可以连接到 Excel、PowerBI、Tableau 等报表工具。
* [弹性事务](/documentation/articles/sql-database-elastic-transactions-overview/)：使用此功能可在 Azure SQL 数据库中跨多个数据库运行事务。弹性数据库事务适用于使用 ADO .NET 的 .NET 应用程序，并且与熟悉的使用 [System.Transaction](https://msdn.microsoft.com/zh-cn/library/system.transactions.aspx) 类的编程体验相集成。

下图显示的体系结构与数据库集合有关的**弹性数据库功能**。

在此图中，数据库颜色表示架构。颜色相同的数据库具有相同的架构。

1. 一组使用分片体系结构的 **Azure SQL 数据库**托管在 Azure 上。
2. **弹性数据库客户端库**用于管理分片集。
3. 一个数据库子集已放入**弹性数据库池**。（请参阅[什么是池？](/documentation/articles/sql-database-elastic-pool/)
4. **弹性数据库作业**针对所有数据库运行计划或即席的 T-SQL 脚本。
5. **拆分/合并工具**用于将数据从一个分片移到另一个分片。
6. 使用**弹性数据库查询**可以编写跨分片集中所有数据库运行的查询。
7. **弹性事务**允许跨多个数据库运行事务。


![弹性数据库工具][1]


## 为什么使用这些工具？

VM 和 blob 存储可以轻松实现云应用程序的弹性和缩放需求 - 只需添加或减少单位，或者增加功率。但对于关系数据库中的有状态数据处理，这仍是一个挑战。在这些情况下出现的难题：

* 增加和减少工作负荷的关系数据库部分的容量。
* 管理可能会影响特定数据子集的热点 - 例如，特别繁忙的最终客户（租户）。

过去以来，在解决此类情况时，一般都是投资更大规模的数据库服务器来支持应用程序。但是，在预定义商品硬件上执行所有处理的云中，此选项受限制。将数据和处理负载分散到许多结构相同的数据库（一种称为“分片”的向外缩放模式），无论在成本还是弹性上，都是超越传统向上缩放方法的另一种选择。

## 横向缩放与纵向缩放

下图显示了缩放的横向和纵向维度，即弹性数据库的基本缩放方法。

![横向缩放与纵向缩放][2]

横向缩放是指添加或删除数据库，以调整容量或整体性能。这也称为“向外缩放”。分片是常用的横向缩放实现方法，它会将数据分区到结构相同的一组数据库上。

纵向缩放是指增加或减少单个数据库的性能级别 – 这也称为“向上缩放”。

大多数云规模的数据库应用程序都使用这两种策略的组合。例如，软件即服务应用程序可能使用横向缩放来预配新的最终客户，并使用纵向缩放来允许每个最终客户的数据库根据工作负荷的需要扩展或缩减资源。

* 可以使用[弹性数据库客户端库](/documentation/articles/sql-database-elastic-database-client-library/)来管理水平缩放。

* 可以通过使用 Azure PowerShell cmdlet 更改服务层或者通过将数据库放入弹性池中，来实现纵向缩放。

## 分片

*分片*是一项可跨许多独立的数据库分发大量相同结构数据的技术。这项技术尤其受到最终客户或企业创建软件即服务 (SAAS) 产品的云开发人员的欢迎。这些最终客户通常称为“租户”。需要分片的原因有很多：

* 数据总量过大而超出单个数据库的限制范围
* 整个工作负荷的事务吞吐量超出单个数据库的容量
* 租户可能需要与其他租户物理隔离，因此每个租户都需要单独的数据库
* 由于合规性、性能或地理政治的原因，不同的数据库部分可能需要驻留在不同的地域中。

在其他方案（例如从分布式设备中引入数据）中，分片可用于填充临时组织的一组数据库。例如，可以每天或每周专门使用某个单独的数据库。在该情况下，分片键可以是一个表示日期的整数（显示在分片表的所有行中），应用程序必须将用于检索有关日期范围的信息的查询路由到涉及相关范围的数据库子集。

应用程序中的每个事务均受限于分片键的单个值时，分片效果最佳。这可以确保所有事务都将本地放置在特定数据库中。

## 多租户和单租户

某些应用程序使用最简单的方法为每个租户创建一个单独的数据库。这就是**单租户分片模式**，它提供了隔离、备份/还原功能以及根据租户粒度进行的资源缩放。借助单租户分片，每个数据库都将与特定租户 ID 值（或客户键值）关联，而该键无需始终出现在数据本身中。应用程序负责将每个请求路由到相应的数据库 - 客户端库可以简化这种操作。

![单租户与多租户][4]

其他方案是将多个租户一同打包到数据库中，而非将其隔离到单独的数据库中。这是典型的**多租户分片模式**，该模式的使用可能取决于应用程序可管理大量极小型租户这一情况的考虑。在多租户分片中，数据库表中的行全都设计为带有可标识租户 ID 的键或分片键。同样，应用程序层负责将租户的请求路由到相应的数据库，而弹性数据库客户端库可以支持这种操作。此外，可以使用行级安全性来筛选每个租户可以访问的行 - 有关详细信息，请参阅该[具有弹性数据库工具和行级安全性的多租户应用程序](/documentation/articles/sql-database-elastic-tools-multi-tenant-row-level-security/)。多租户分片模式可能需要在数据库之间重新分配数据，而弹性数据库拆分/合并工具正好可以帮助实现此目的。若要深入了解如何通过弹性池设计 SaaS 应用程序，请参阅[多租户 SaaS 应用程序和 Azure SQL 数据库的设计模式](/documentation/articles/sql-database-design-patterns-multi-tenancy-saas-applications/)。

### 将数据从多租户数据库移到单租户数据库

创建 SaaS 应用程序时，通常会向潜在客户提供试用版本。在此情况下，使用多租户数据库来处理数据较符合成本效益。不过，当潜在客户成为真正客户后，单租户数据库就更好，因为它提供更好的性能。如果客户在试用期间创建了数据，可以使用[拆分/合并工具](/documentation/articles/sql-database-elastic-scale-overview-split-and-merge/)将数据从多租户数据库移到新的单租户数据库。

## 后续步骤

有关演示客户端库的示例应用，请参阅[弹性数据库工具入门](/documentation/articles/sql-database-elastic-scale-get-started/)。

若要转换现有的数据库以使用该工具，请参阅[迁移要扩展的现有数据库](/documentation/articles/sql-database-elastic-convert-to-use-elastic-tools/)。

若要查看弹性数据库池的具体信息，请参阅[弹性数据库池的价格和性能注意事项](/documentation/articles/sql-database-elastic-pool-guidance/)，或者参考[教程](/documentation/articles/sql-database-elastic-pool-create-portal/)创建新池。

[AZURE.INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Anchors-->

<!--Image references-->

[1]: ./media/sql-database-elastic-scale-introduction/tools.png
[2]: ./media/sql-database-elastic-scale-introduction/h_versus_vert.png
[3]: ./media/sql-database-elastic-scale-introduction/overview.png
[4]: ./media/sql-database-elastic-scale-introduction/single_v_multi_tenant.png

<!---HONumber=Mooncake_Quality_Review_1118_2016-->