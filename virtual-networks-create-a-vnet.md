<properties
   pageTitle="创建虚拟网络"
   description="指导你完成相关步骤以轻松创建基本虚拟网络。"
   services="virtual-network"
   documentationCenter=""
   authors="telmos"
   manager="carolz"
   editor="tysonn"/>  


<tags
   ms.service="virtual-network"
   ms.date="07/06/2015"
   wacn.date=""/>  


# 创建虚拟网络

在创建虚拟网络时，虚拟网络中的服务和 VM 不必通过 Internet 就可以相互安全通信。创建仅限云的专用虚拟网络是一个相对快速而简单的过程。由于仅限云的虚拟网络不适用于跨界连接，因此你不需要获取和配置 VPN 设备或身份验证证书。

创建虚拟网络后，可以向其添加新的 VM 和 PaaS 实例。请注意，如果使用管理门户来创建 VM，请务必选择“从库中”，以便可以指定虚拟网络。这很重要，因为创建虚拟机后，将不能返回，因此无法再将 VM 放在虚拟网络中。

[Azure Note] **使用此过程创建仅限云的专用虚拟网络。** 由于创建跨界配置会增加复杂性，因此请勿使用此过程创建以后将连接到本地网络的虚拟网络。如果要在 Azure 与本地网络之间创建安全跨界连接，请参阅[关于安全跨界连接](https://msdn.microsoft.com/zh-cn/library/azure/dn133798.aspx)。

## 创建虚拟网络

1. 登录到**管理门户**。
2. 在屏幕左下角，单击“新建”。在导航窗格中，单击“网络服务”，然后单击“虚拟网络”。单击“自定义创建”以启动配置向导。
3. 在“虚拟网络详细信息”页上，输入以下信息，然后单击右下角的“下一步”箭头。有关详细信息页上设置的详细信息，请参阅[如何管理 VNet 属性](/documentation/articles/virtual-networks-settings)中的**虚拟网络详细信息**部分。
	-  **名称：**为虚拟网络命名。部署 VM 和服务时，将使用此虚拟网络名称，因此最好不要使用太复杂的名称。

	-  **区域：**从下拉列表中，选择所需的区域。将在指定区域的 Azure 数据中心创建虚拟网络。



4. 在“DNS 服务器和 VPN 连接”页上，不要进行任何更改。只需单击箭头，转到下一页。默认情况下，Azure 将为虚拟网络提供基本名称解析。解析你的名称可能比较复杂，导致基本 Azure 名称解析服务无法处理。在这种情况下，你以后可能会想要将运行 DNS 的虚拟机添加到虚拟网络中。有关 Azure 名称解析和 DNS 的详细信息，请参阅[名称解析](/documentation/articles/virtual-networks-name-resolution-for-vms-and-role-instances)。
5. 在“虚拟网络地址空间”页上，可输入要用于此 VNet 的地址空间。除非要为 VM 使用特定内部 IP 地址范围，或者要为接收静态 DIP 的 VM 创建特定的子网，否则不需要在此页上进行任何更改。如果一定要创建多个子网，则在此页上单击“添加子网”即可添加。有关详细信息页上的设置的详细信息，请参阅[如何管理 VNet 属性](/documentation/articles/virtual-networks-settings)中的**虚拟网络详细信息**部分。

	-  有关详细信息页上的设置的详细信息，请参阅[如何管理 VNet 属性](/documentation/articles/virtual-networks-settings)中的**虚拟网络详细信息**部分。
	-  由于你不会使用跨界 VPN 配置将此专用虚拟网络连接到你的本地网络，因此不需要将这些设置与现有的本地网络 IP 地址范围进行协调。如果你以后可能需要创建跨界配置，则现在需要将地址空间与本地站点中已存在的地址范围进行协调，以免出现路由问题。以后更改范围可能会比较复杂，并且通常必须重新部署


6. 单击“虚拟网络地址空间”页右下角的复选标记，即可开始创建虚拟网络。创建虚拟网络后，在管理门户的网络页上，你将看到“状态”下面列出“已创建”。
7. 虚拟网络创建完成后，即可在其中进行部署。例如，如果想要将 VM 部署到 VNet，请参阅[如何创建自定义 VM](/documentation/articles/virtual-machines-create-custom)。创建新 VM 时，请务必选择“从库中”，以便显示选择虚拟网络的选项。请注意，如果已部署现有 VM 和 PaaS 实例，则不能直接将它们移到新的虚拟网络。这是因为在部署过程中已为它们配置网络配置设置。你必须重新将它们部署到新的虚拟网络。



## 后续步骤
-  了解有关 Azure 中的[虚拟网络](/documentation/articles/virtual-networks-overview)的详细信息。 

-  在虚拟网络中[添加虚拟机](/documentation/articles/virtual-machines-create-custom)。

<!---HONumber=Mooncake_Quality_Review_1118_2016-->