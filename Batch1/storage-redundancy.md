<properties
	pageTitle="Azure 存储复制 | Azure"
	description="复制 Microsoft Azure 存储帐户中的数据以实现持久性和高可用性。复制选项包括本地冗余存储 (LRS)、区域冗余存储 (ZRS)、异地冗余存储 (GRS) 和读取访问异地冗余存储 (RA-GRS)。"
	services="storage"
	documentationCenter=""
	authors="tamram"
	manager="carmonm"
	editor="tysonn"/>  


<tags
	ms.service="storage"
	ms.workload="storage"
	ms.tgt_pltfrm="na"
	ms.devlang="na"
	ms.topic="article"
	ms.date="09/21/2016"
	ms.author="jutang;tamram"/>

# Azure 存储复制

始终复制 Microsoft Azure 存储帐户中的数据以确保持久性和高可用性，即使在遇到临时硬件故障时也能符合 [Azure 存储 SLA](/support/sla/storage/) 要求。

创建存储帐户时，必须选择以下复制选项之一：

- [本地冗余存储 (LRS)](#locally-redundant-storage)
- [区域冗余存储空间 (ZRS)](#zone-redundant-storage)
- [异地冗余存储 (GRS)](#geo-redundant-storage)
- [读取访问异地冗余存储 (RA-GRS)](#read-access-geo-redundant-storage)

下表简要概述了 LRS、ZRS、GRS 和 RA-GRS 之间的差异，而后续章节将详细介绍每种类型的复制。


| 复制策略 | LRS | GRS | RA-GRS |
|:-----------------------------------------------------------------------------------|:----|:----|:-------|
| 数据在多个设施之间进行复制。 | 否 | 是 | 是 |
| 可以从次要位置和主位置读取数据。 | 否 | 否 | 是 |
| 在单独的节点上维护的数据副本数。 | 3 | 6 | 6 |

有关不同冗余选项的定价信息，请参阅 [Azure 存储空间定价](/pricing/details/storage/)。

>[AZURE.NOTE] 高级存储仅支持本地冗余存储 (LRS)。有关高级存储的信息，请参阅[高级存储：适用于 Azure 虚拟机工作负荷的高性能存储](/documentation/articles/storage-premium-storage/)。

## 本地冗余存储

本地冗余存储 (LRS) 在创建存储帐户所在的区域中复制数据。为最大程度地提高持久性，针对存储帐户中的数据发出的每个请求将复制三次。这三个副本每个都驻留在不同的容错域和升级域中。容错域 (FD) 是一组代表出错的物理单元的节点，可将其视为属于同一物理机架的节点。升级域 (UD) 是一组在服务升级（推出）过程中一起升级的节点。三个副本将分布在 UD 和 FD 上，以确保即使在硬件故障影响单个机架，以及在推出期间升级节点时，数据也可用。请求仅在写入所有三个副本后，才成功返回。

虽然对于大多数应用程序建议使用异地冗余存储 (GRS)，但是在某些情况下可能需要本地冗余存储：

- 与 GRS 相比，LRS 成本更低，同时还提供更高的吞吐量。如果应用程序存储可轻松重构的数据，则可以选择 LRS。

- 由于数据治理需要，某些应用程序被限制为只能在单个区域内复制数据。

- 如果应用程序具有自己的异地复制策略，则可能不需要 GRS。




## 异地冗余存储

异地冗余存储 (GRS) 将数据复制到距主要区域数百英里以外的次要区域。如果存储帐户启用了 GRS，即使在遇到区域完全停电或导致主要区域不可恢复的灾难时，数据也能持久保存。

对于启用了 GRS 的存储帐户，更新将首先提交到主要区域，并在其中复制三次。然后，更新将复制到次要区域（也是在其中复制三次），并且是在不同的容错域和升级域之间复制。

> [AZURE.NOTE] 使用 GRS 时，写入数据请求将异步复制到次要区域。请务必注意，选择 GRS 不会影响针对主要区域发出的请求的延迟。但是，由于异步复制涉及延迟，因此在遇到区域性灾难时，如果无法将数据从主要区域中恢复，则尚未复制到次要区域的更改可能会丢失。
 
创建存储帐户时，可以为帐户选择主要区域。次要区域是根据主要区域确定的且无法更改。下表显示了配对的主要区域和次要区域。

|主要 |次要
| ---------------   |----------------
|中国北部 |中国东部
|中国东部 |中国北部 
 
## 读取访问异地冗余存储

除了在 GRS 所提供的两个区域之间进行复制外，读取访问异地冗余存储 (RA-GRS) 还提供对次要位置中的数据的只读访问权限，从而在最大程度上提高存储帐户的可用性。当主要区域中的数据不可用时，应用程序可以从次要区域读取数据。

当启用对次要区域中的数据的只读访问权限时，除了存储帐户的主终结点外，还可以在辅助终结点上获取数据。辅助终结点与主终结点类似，但会在帐户名称后面追加后缀 `–secondary`。例如，如果 Blob 服务的主终结点是 `myaccount.blob.core.windows.net`，辅助终结点则是 `myaccount-secondary.blob.core.windows.net`。存储帐户的访问密钥对于主终结点和辅助终结点是相同的。

## 后续步骤

- [Azure 存储定价](/pricing/details/storage/)
- [关于 Azure 存储帐户](/documentation/articles/storage-create-storage-account/)
- [Azure 存储可伸缩性和性能目标](/documentation/articles/storage-scalability-targets/)
- [Microsoft Azure Storage Redundancy Options and Read Access Geo Redundant Storage（Microsoft Azure 存储冗余选项和读取访问异地冗余存储）](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
- [SOSP 论文 - Azure 存储空间：具有高度一致性的高可用云存储服务](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)
 

<!---HONumber=Mooncake_Quality_Review_1118_2016-->