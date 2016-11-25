<properties
	pageTitle="在 Azure 中使用 Visual Studio Team Services 进行持续交付 | Microsoft Azure"
	description="了解如何将 Visual Studio Team Services 团队项目配置为自动生成并部署到 Azure App Service 或云服务中的 Web 应用功能。"
	services="cloud-services"
	documentationCenter=".net"
	authors="TomArcher"
	manager="douge"
	editor=""/>  


<tags
	ms.service="cloud-services"
	ms.workload="tbd"
	ms.tgt_pltfrm="na"
	ms.devlang="dotnet"
	ms.topic="article"
	ms.date="02/03/2016"
	ms.author="tarcher"/>

# 使用 Visual Studio Team Services 向 Azure 持续交付

可将 Visual Studio Team Services 团队项目配置为自动生成并部署到 Azure Web 应用或云服务。有关如何使用*本地* Team Foundation Server 设置持续生成和部署系统的信息，请参阅[在 Azure 中持续交付云服务](cloud-services-dotnet-continuous-delivery.md)。

本教程假设你已安装 Visual Studio 2013 和 Azure SDK。如果尚未安装 Visual Studio 2013，请在 [www.visualstudio.com](http://www.visualstudio.com) 选择“免费试用”链接以下载该软件。从[此处](http://go.microsoft.com/fwlink/?LinkId=239540)安装 Azure SDK。

> [AZURE.NOTE] 需要使用 Visual Studio Team Services 帐户才能完成本教程：可[免费开启 Visual Studio Team Services 帐户](http://go.microsoft.com/fwlink/p/?LinkId=512979)。

若要使用 Visual Studio Team Services 将云服务设置为自动生成并部署到 Azure，请执行下列步骤：

## 步骤 1：创建团队项目

按照[此处](http://go.microsoft.com/fwlink/?LinkId=512980)的说明创建团队项目，并将其链接到 Visual Studio。本演练假设你使用 Team Foundation 版本控制 (TFVC) 作为源代码管理解决方案。若要使用 Git 进行版本控制，请参阅[本演练的 Git 版本](http://go.microsoft.com/fwlink/p/?LinkId=397358)。

## 步骤 2：将项目签入到源代码管理

1. 在 Visual Studio 中，打开要部署的解决方案或新建解决方案。可通过执行本演练中的步骤来部署 Web 应用或云服务（Azure 应用程序）。若要创建新的解决方案，请创建新的 Azure 云服务项目或新的 ASP.NET MVC 项目。确保项目以 .NET Framework 4 或 4.5 为目标。若要创建云服务项目，请添加 ASP.NET MVC Web 角色和辅助角色，并为 Web 角色选择 Internet 应用程序。系统提示时，请选择“Internet 应用程序”。如果要创建 Web 应用，请选择 ASP.NET Web 应用程序项目模板，然后选择 MVC。请参阅[在 Azure App Service 中创建 ASP.NET Web 应用](/app-service-web/web-sites-dotnet-get-started.md)

	> [AZURE.NOTE] Visual Studio Team Services 目前仅支持 Visual Studio Web 应用程序的 CI 部署。网站项目不在支持范围内。

1. 打开解决方案的上下文菜单，然后选择“将解决方案添加到源代码管理”。

	![][5]

1. 接受或更改默认值，然后选择“确定”按钮。此过程完成后，解决方案资源管理器中即显示源代码管理图标。

	![][6]

1. 打开解决方案的快捷菜单，然后选择“签入”。

	![][7]

1. 在团队资源管理器的“挂起的更改”区域中，为签入键入注释并选择“签入”按钮。

	![][8]

	记下在签入时用于包含或排除特定更改的选项。如果已排除所需的更改，请选择“全部包含”链接。

	![][9]

## 步骤 3：将项目连接到 Azure

1. 拥有包含源代码的 VS Team Services 团队项目，即可将其连接到 Azure。在 [Azure 经典门户](http://manage.windowsazure.com)中选择云服务或 Web 应用，或通过选择左下角的“+”图标再选择“云服务”或“Web 应用”，然后选择“快速创建”来创建新的云服务或 Web 应用。选择“使用 Visual Studio Team Services 设置发布”链接。

	![][10]

1. 在向导中，在文本框中键入 Visual Studio Team Services 帐户的名称，然后单击“立即授权”链接。可能会要求登录。

	![][11]

1. 在“连接请求”弹出对话框中，选择“接受”按钮以授权 Azure 在 VS Team Services 中配置团队项目。

	![][12]

1. 授权成功后，将显示一个包含一系列 Visual Studio Team Services 团队项目的下拉列表。选择在之前的步骤中创建的团队项目的名称，然后选择向导的复选标记按钮。

	![][13]

1. 链接项目后，可看到将更改签入 Visual Studio Team Services 团队项目的相关说明。下次签入时，Visual Studio Team Services 将生成项目并将其部署到 Azure。通过单击“通过 Visual Studio 签入”链接并单击“启动 Visual Studio”链接（或位于门户屏幕底部具有等效功能的“Visual Studio”按钮）可立即尝试此操作。

	![][14]

## 步骤 4：触发重新生成并重新部署项目

1. 在 Visual Studio 的团队资源管理器中，选择“源代码管理资源管理器”链接。

	![][15]

1. 导航到解决方案文件并将其打开。

	![][16]

1. 在**解决方案资源管理器**中，打开文件并进行更改。例如，更改 MVC Web 角色中 Views\\Shared 文件夹下的文件 `_Layout.cshtml`。

	![][17]

1. 编辑站点的徽标，并选择 **Ctrl+S** 来保存文件。

	![][18]

1. 在“团队资源管理器”中，选择“挂起的更改”链接。

	![][19]

1. 输入注释，然后选择“签入”按钮。

	![][20]

1. 选择“主页”按钮可返回**团队资源管理器**主页。

	![][21]

1. 选择“生成”链接可查看正在进行的生成。

	![][22]

	**团队资源管理器**将显示已为签入触发生成。

	![][23]

1. 双击正在进行的生成的名称可在生成进行中查看详细日志。

	![][24]

1. 生成正在进行时，可使用向导查看将 TFS 链接到 Azure 时创建的生成定义。打开生成定义的快捷菜单，然后选择“编辑生成定义”。

	![][25]

	在“触发器”选项卡中，可看到已默认设置为在每次签入时生成生成定义。

	![][26]

	在“进程”选项卡中，可看到已将部署环境设置为云服务或 Web 应用的名称。如果正在处理 Web 应用，看到的属性将不同于此处所示。

	![][27]

1. 若要使用默认值以外的值，请指定属性的值。Azure 发布属性在 **Deployment** 部分中。

	下表显示了 **Deployment** 部分中的可用属性：

	|属性|默认值|
	|---|---|
	|允许不受信任的证书|如果为 false，则 SSL 证书必须由根颁发机构签名。|
	|允许升级|允许部署更新现有的部署，而不允许创建新部署。保留 IP 地址。|
	|不要删除|如果为 true，则不会覆盖现有的无关部署（允许升级）。|
	|部署设置的路径|Web 应用的 .pubxml 文件的路径，相对于存储库的根文件夹。对于云服务将忽略该属性。|
	|Sharepoint 部署环境|与服务名称相同。|
	|Azure 部署环境|Web 应用或云服务的名称|

1. 如果使用多个服务配置（.cscfg 文件），可以在“生成”>“高级”>“MSBuild 参数”设置中指定所需的服务配置。例如，若要使用 ServiceConfiguration.Test.cscfg，请设置 MSBuild 参数行选项 `/p:TargetProfile=Test`。

	![][38]

	此时，生成应已成功完成。

	![][28]

1. 如果双击生成名称，则 Visual Studio 将显示“生成摘要”，其中包括来自关联的单元测试项目的任何测试结果。

	![][29]

1. 在 [Azure 经典门户](http://manage.windowsazure.com)中，可以在选定过渡环境后在“部署”选项卡上查看关联的部署。

	![][30]

1.	浏览到网站的 URL。对于 Web 应用，单击命令栏上的“浏览”按钮即可。对于云服务，请选择显示云服务过渡环境的“仪表板”页面上“速览”部分中的 URL。默认情况下，来自云服务的持续集成的部署将发布到过渡环境。可将“备用云服务环境”属性设置为“生产”以进行更改。以下屏幕截图显示了站点 URL 在云服务仪表板页上的位置。

	![][31]

	新的浏览器选项卡随即打开，以显示正在运行的网站。

	![][32]

	对于云服务，如果对项目进行其他更改，则将触发更多生成，并且将累积多个部署。标记为“活动”的最新项目。

	![][33]

## 步骤 5：重新部署以前的生成

此步骤是适用于云服务的可选步骤。在 Azure 经典门户中，选择以前的部署，然后选择“重新部署”按钮可使站点退回以前的签入。请注意，这将在 TFS 中触发新的生成，并在部署历史记录中创建新的条目。

![][34]

## 步骤 6：更改生产部署

此步骤仅适用于云服务，而不适用于 Web 应用。准备就绪后，可在 Azure 经典门户中选择“交换”按钮，以将过渡环境提升为生产环境。新部署的过渡环境将提升为生产环境，而之前的生产环境（如果有）将变成过渡环境。虽然生产环境和过渡环境的活动部署可能会不同，但无论是何种环境，最新生成的部署历史记录都相同。

![][35]

## 步骤 7：运行单元测试

此步骤仅适用于 Web 应用，而不适用于云服务。若要对实时部署或过渡部署进行质量把关，可运行单元测试，并在测试失败时停止部署。

1.  在 Visual Studio 中添加单元测试项目。

	![][39]

1.  添加对要测试的项目的项目引用。

	![][40]

1.  添加单元测试。若要开始，请先尝试始终会通过的虚拟测试。

		```
		using System;
		using Microsoft.VisualStudio.TestTools.UnitTesting;

		namespace UnitTestProject1
		{
		    [TestClass]
		    public class UnitTest1
		    {
		        [TestMethod]
		        [ExpectedException(typeof(NotImplementedException))]
		        public void TestMethod1()
		        {
		            throw new NotImplementedException();
		        }
		    }
		}
		```

1.  编辑生成定义，选择“进程”选项卡，然后展开“测试”节点。

1.  将“测试失败则生成失败”设置为 True。这意味着除非通过测试，否则将不会进行部署。

	![][41]

1.  将新的生成排队。

	![][42]

	![][43]

1. 在生成过程中查看其进度。

	![][44]

	![][45]

1. 生成完成后查看测试结果。

	![][46]

	![][47]

1.  尝试创建会失败的测试。复制第一个测试并将其重命名，注释不使用声明 NotImplementedException 为预期异常的代码行，以添加新的测试。

		```
		[TestMethod]
		//[ExpectedException(typeof(NotImplementedException))]
		public void TestMethod2()
		{
		    throw new NotImplementedException();
		}
		```

1. 签入更改以将新的生成排队。

	![][48]

1. 查看测试结果，以了解有关失败的详细信息。

	![][49]

	![][50]

## 后续步骤
有关 Visual Studio Team Services 中的单元测试的详细信息，请参阅 [在生成中运行单元测试](http://go.microsoft.com/fwlink/p/?LinkId=510474)。如果使用 Git，请参阅[在 Git 中共享代码](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx)和[使用 GIT 在 Azure App Service 中进行持续部署](/app-service-web/web-sites-publish-source-control.md)。有关 Visual Studio Team Services 的详细信息，请参阅 [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861)。

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG

<!---HONumber=Mooncake_Quality_Review_1118_2016-->