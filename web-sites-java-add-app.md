<properties 
	pageTitle="将 Java 应用程序添加到 Azure 网站" 
	description="本教程演示如何将页面或应用程序添加到已配置为使用 Java 的 Azure 网站实例。" 
	services="app-service\web" 
	documentationCenter="java" 
	authors="rmcmurray" 
	manager="wpickett" 
	editor="jimbe"/>  


<tags 
	ms.service="app-service-web" 
	ms.date="08/31/2015" 
	wacn.date=""/>  


# 将 Java 应用程序添加到 Azure 网站

按照[在 Azure 网站中创建 Java Web 应用](/documentation/articles/web-sites-java-get-started)中的说明初始化 Java 网站后，可通过将 WAR 放置在 **webapps** 文件夹上载应用程序。

**webapps** 文件夹的导航路径因设置网站的方式而有所不同。

- 如果使用 Azure 配置 UI 设置 Web 应用，则 **webapps** 文件夹的路径格式为 **d:\\home\\site\\wwwroot\\webapps**。 

请注意，可使用源代码管理上载应用程序或网页，即使在连续集成方案中亦是如此。有关结合使用源代码管理和网站的说明，请参阅[从源代码管理发布到 Azure 网站](../web-sites-publish-source-control)。还可以选择 FTP 上载应用程序或网页。

Tomcat 网站说明：将 WAR 文件上载到 **webapps** 文件夹后，Tomcat 应用服务器会检测到已添加该文件并自动上载。请注意，如果将文件（除 WAR 文件以外）复制到 ROOT 目录，在使用这些文件之前，将需要重新启动该应用服务器。在 Azure 上运行的 Tomcat Java 网站的自动上载功能基于添加的新 WAR 文件，或添加到 **webapps** 文件夹的新文件或目录。

<!---HONumber=Mooncake_Quality_Review_1118_2016-->