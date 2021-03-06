<!-- not suitable for Mooncake -->


<properties 
	pageTitle="HDInsight 中的 Apache Spark 概述 | Azure" 
	description="介绍 HDInsight 中的 Apache Spark，以及可在应用程序中使用 HDInsight 上的 Spark 的情况。" 
	services="hdinsight" 
	documentationCenter="" 
	authors="nitinme" 
	manager="paulettm" 
	editor="cgronlun"
	tags="azure-portal"/>

<tags
	ms.service="hdinsight"
	ms.date="06/06/2016"
	wacn.date=""/>

# 概述：HDInsight Linux 上的 Apache Spark
 
<a href="http://spark.apache.org/" target="_blank">Apache Spark</a> 是一种开放源代码并行处理框架，支持内存中处理，以提升大数据分析应用程序的性能。Spark 处理引擎是专为速度、易用性和复杂分析打造的产品。Spark 的内存中计算功能使其成为机器学习和图形计算中的迭代算法的最佳选择。Spark 也能与 Azure Blob 存储 (WASB) 兼容，因此可通过 Spark 轻松处理存储在 Azure 中的现有数据。

在 HDInsight 中创建 Spark 群集时，即会创建 Azure 计算资源并安装和配置 Spark。在 HDInsight 中创建 Spark 群集只需要约十分钟。系统将要处理的数据存储在 Azure Blob 存储中。请参阅[将 Azure Blob 存储与 HDInsight 配合使用][hdinsight-storage]。

![Azure HDInsight 上的 Apache Spark](./media/hdinsight-apache-spark-overview/hdispark.architecture.png "Azure HDInsight 上的 Apache Spark")


**想要开始在 Azure HDInsight 上使用 Apache Spark？** 请参阅[快速入门：使用 Jupyter 在 HDInsight Linux 上创建 Spark 群集并运行示例应用程序](/documentation/articles/hdinsight-apache-spark-jupyter-spark-sql)。

>[AZURE.NOTE] 有关当前版本的已知问题和限制列表，请参阅[Azure HDInsight (Linux) 中 Apache Spark 的已知问题](/documentation/articles/hdinsight-apache-spark-jupyter-spark-sql)。


## 为何要在 Azure HDInsight 上使用 Spark？ 

Azure HDInsight 提供完全托管的 Spark 服务。在 HDInsight 上使用 Spark 的好处如下：

| 功能 | 说明 |
|-------------------------------------|-------------------|
| 方便创建群集 | 可使用 Azure 管理门户、Azure PowerShell 或 HDInsight .NET SDK，在几分钟之内于 HDInsight 上创建新的 Spark 群集。请参阅 [HDInsight 中的 Spark 群集入门](/documentation/articles/hdinsight-apache-spark-jupyter-spark-sql) |
| 易于使用 | HDInsight 群集中的 Spark 包含预先配置的 Jupyter 笔记本。可使用这些笔记本执行交互式数据处理和可视化。URL 为 https://CLUSTERNAME.azurehdinsight.cn/jupyter。将 __CLUSTERNAME__ 替换为 Spark HDInsight 群集的名称。|
| REST API | HDInsight 中的 Spark 包含 [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)，它是基于 REST-API 的 Spark 作业服务器，用于远程提交和监视正在运行的作业。 |
| 支持 Azure Data Lake Store | 可将 HDInsight 上的 Spark 配置为使用 Azure Data Lake Store 作为附加存储。有关 Data Lake Store 的详细信息，请参阅 [Azure Data Lake Store 概述](/documentation/articles/data-lake-store-overview)。
| 与 Azure 服务集成 | HDInsight 上的 Spark 随附了 Azure 事件中心的连接器。除了 Spark 提供的 [Kafka](http://kafka.apache.org/) 之外，客户还可以使用事件中心来生成流式处理应用程序。 |
| 支持 R Server | 可以在 HDInsight Spark 群集上设置 R Server，以 Spark 群集承诺的速度运行分布式 R 计算。有关详细信息，请参阅[开始使用 HDInsight 上的 R Server](/documentation/articles/hdinsight-hadoop-r-server-get-started)。 |
| 与 IntelliJ IDEA 集成 | 可以使用 IntelliJ 的 HDInsight 插件来创建应用程序，并将应用程序提交到 HDInsight Spark 群集。有关详细信息，请参阅[使用 IntelliJ IDEA 的 HDInsight 工具插件为 HDInsight Spark Linux 群集创建 Spark 应用程序](/documentation/articles/hdinsight-apache-spark-intellij-tool-plugin)。 |
| 并发查询 | HDInsight 中的 Spark 支持并发查询。这让来自一个用户、多个用户和多个应用程序的多个查询可共享相同的群集资源。 |
| SSD 缓存 | 可选择将数据缓存在内存中，或缓存在已附加到群集节点的 SSD 中。内存缓存提供的查询性能最佳但可能费用昂贵；SSD 缓存是改善查询性能的绝佳选项，而且无需创建可容纳内存中整个数据集的规模的群集。|
| 与 BI 工具集成 | HDInsight 上的 Spark 提供用于数据分析的 BI 工具（如[Power BI](http://www.powerbi.com/) 和 [Tableau](http://www.tableau.com/products/desktop)）连接器。|
| 预加载的 Anaconda 库 | HDInsight 上的 Spark 群集随附预安装的 Anaconda 库。[Anaconda](http://docs.continuum.io/anaconda/) 提供将近 200 个用于机器学习、数据分析、可视化等的库。|
| 可伸缩性 | 虽然可以在创建过程中指定群集中的节点数，但可能需要扩大或收缩群集以匹配工作负载。所有 HDInsight 群集都允许更改群集中的节点数。此外，由于所有数据都存储在 Azure Blob 存储中，因此可在不丢失数据的情况下删除 Spark 群集。 |
| 全天候支持 | HDInsight 上的 Spark 提供全天候企业级支持，并提供保证正常运行时间达 99.9% 的 SLA。|



## HDInsight 上的 Spark 有哪些用例？

HDInsight 中的 Apache Spark 适用于以下主要方案。

### 交互式数据分析和 BI

[观看教程](/documentation/articles/hdinsight-apache-spark-use-bi-tools)

HDInsight 中的 Apache Spark 将数据存储在 Azure Blob 内。商务专家和重要决策者可以利用这些数据来进行分析和创建报告，并使用 Microsoft Power BI 来根据分析数据生成交互式报告。分析师可以从 Azure 存储空间内的非结构化/半结构化数据着手、使用笔记本来定义数据的架构，然后使用 Microsoft Power BI 生成数据模型。HDInsight 中的 Spark 还支持 Tableau、Qlikview 和 SAP Lumira 等多种第三方 BI 工具，因此能成为数据分析师、商务专家和重要决策者的理想平台。

### 迭代机器学习

[查看教程：使用 HVAC 数据预测建筑物温度](/documentation/articles/hdinsight-apache-spark-ipython-notebook-machine-learning)

[查看教程：预测食品检测结果](/documentation/articles/hdinsight-apache-spark-machine-learning-mllib-ipython)

Apache Spark 随附 [MLlib](http://spark.apache.org/mllib/) - 构建在 Spark 基础之上的机器学习库。此外，HDInsight 上的 Spark 还包含 Anaconda - 为机器学习提供各种包的 Python 分发版。结合内置的 Jupyter 笔记本支持，你将拥有最先进的机器学习应用程序创建环境。

### 流式处理和实时数据分析

[观看教程](/documentation/articles/hdinsight-apache-spark-eventhub-streaming)

实时数据分析可用于多种情景，从通过在数据抵达时进行处理来缩短获取数据见解的时间，到生成真正的流式处理解决方案皆可使用。HDInsight 中的 Spark 提供丰富的支持供你生成实时分析解决方案。Spark 提供从 Kafka、Flume、Twitter、ZeroMQ 或 TCP 套接字等众多来源引入数据的连接器，而 HDInsight 中的 Spark 还增加了对从 Azure 事件中心引入数据的一流支持。事件中心是 Azure 上最广泛使用的队列服务。拥有立即可用的事件中心支持，让 HDInsight 中的 Spark 成为生成实时分析管道的理想平台。

##<a name="next-steps"></a>Spark 群集包含哪些组件？

默认情况下，HDInsight 中的 Spark 可通过群集提供以下组件。

- [Spark Core](https://spark.apache.org/docs/1.5.1/)。包括 Spark Core、Spark SQL、Spark 流式处理 API、GraphX 和 MLlib。
- [Anaconda](http://docs.continuum.io/anaconda/)
- [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
- [Jupyter 笔记本](https://jupyter.org)

HDInsight 中的 Spark 还提供 [ODBC 驱动程序](http://go.microsoft.com/fwlink/?LinkId=616229)，可用户从 Microsoft Power BI 和 Tableau 等 BI 工具连接到 HDInsight 中的 Spark 群集。

## 从何入手？

首先，请在 HDInsight Linux 上创建 Spark 群集。请参阅[快速入门：使用 Jupyter 在 HDInsight Linux 上创建 Spark 群集并运行示例应用程序](/documentation/articles/hdinsight-apache-spark-jupyter-spark-sql)。

## 后续步骤

### 方案

* [Spark 和 BI：使用 HDInsight 中的 Spark 和 BI 工具执行交互式数据分析](/documentation/articles/hdinsight-apache-spark-use-bi-tools)

* [Spark 和机器学习：使用 HDInsight 中的 Spark 对使用 HVAC 数据生成温度进行分析](/documentation/articles/hdinsight-apache-spark-ipython-notebook-machine-learning)

* [Spark 和机器学习：使用 HDInsight 中的 Spark 预测食品检查结果](/documentation/articles/hdinsight-apache-spark-machine-learning-mllib-ipython)

* [Spark 流式处理：使用 HDInsight 中的 Spark 生成实时流式处理应用程序](/documentation/articles/hdinsight-apache-spark-eventhub-streaming)

* [使用 HDInsight 中的 Spark 分析网站日志](/documentation/articles/hdinsight-apache-spark-custom-library-website-log-analysis)

### 创建和运行应用程序

* [使用 Scala 创建独立的应用程序](/documentation/articles/hdinsight-apache-spark-create-standalone-application)

* [使用 Livy 在 Spark 群集中远程运行作业](/documentation/articles/hdinsight-apache-spark-livy-rest-interface)

### 工具和扩展

* [使用适用于 IntelliJ IDEA 的 HDInsight 工具插件创建和提交 Spark Scala 应用程序](/documentation/articles/hdinsight-apache-spark-intellij-tool-plugin)

* [Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely（使用 IntelliJ IDEA 的 HDInsight 工具插件远程调试 Spark 应用程序）](/documentation/articles/hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely)

* [在 HDInsight 上的 Spark 群集中使用 Zeppelin 笔记本](/documentation/articles/hdinsight-apache-spark-use-zeppelin-notebook)

* [在 HDInsight 的 Spark 群集中可用于 Jupyter 笔记本的内核](/documentation/articles/hdinsight-apache-spark-jupyter-notebook-kernels)

* [Use external packages with Jupyter notebooks（将外部包与 Jupyter 笔记本配合使用）](/documentation/articles/hdinsight-apache-spark-jupyter-notebook-use-external-packages)

* [Install Jupyter on your computer and connect to an HDInsight Spark cluster（在计算机上安装 Jupyter 并连接到 HDInsight Spark 群集）](/documentation/articles/hdinsight-apache-spark-jupyter-notebook-install-locally)

### 管理资源

* [管理 Azure HDInsight 中 Apache Spark 群集的资源](/documentation/articles/hdinsight-apache-spark-resource-manager)

* [跟踪和调试 HDInsight 中的 Apache Spark 群集上运行的作业](/documentation/articles/hdinsight-apache-spark-job-debugging)


[hdinsight-storage]: /documentation/articles/hdinsight-hadoop-use-blob-storage

<!---HONumber=Mooncake_Quality_Review_1118_2016-->