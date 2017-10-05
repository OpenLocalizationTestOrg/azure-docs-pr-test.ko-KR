---
title: "HDInsight에서 Hadoop을 통해 Windows PC 사용 - Azure | Microsoft Docs"
description: "HDInsight에서 Hadoop의 Windows PC에서 작업. PowerShell, Visual Studio 및 Linux 도구를 사용하는 클러스터를 관리 및 쿼리합니다. .NET을 사용하는 빅 데이터 솔루션을 개발합니다."
services: hdinsight
keywords: hadoop on windows,hadoop for windows
author: cjgronlund
manager: jhubbard
ms.author: cgronlun
ms.date: 05/17/2017
ms.topic: article
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.openlocfilehash: e4f231c1f9b903d6cc7f2b062b30d2a072be8493
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="work-in-the-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a><span data-ttu-id="f334b-106">Windows PC에서 HDInsight의 Hadoop 에코시스템 작업</span><span class="sxs-lookup"><span data-stu-id="f334b-106">Work in the Hadoop ecosystem on HDInsight from a Windows PC</span></span>

<span data-ttu-id="f334b-107">HDInsight의 Hadoop 에코시스템 작업을 위한 Windows PC의 개발 및 관리 옵션에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-107">Learn about development and management options on the Windows PC for working in the Hadoop ecosystem on HDInsight.</span></span> 

<span data-ttu-id="f334b-108">HDInsight는 Apache Hadoop 및 Hadoop 구성 요소, Linux에서 개발된 오픈 소스 기술을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-108">HDInsight is based on Apache Hadoop and Hadoop components, open-source technologies developed on Linux.</span></span> <span data-ttu-id="f334b-109">HDInsight 버전 3.4 이상에서는 클러스터에 대한 기본 OS로 Ubuntu Linux 배포를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-109">HDInsight version 3.4 and higher uses the Ubuntu Linux distribution as the underlying OS for the cluster.</span></span> <span data-ttu-id="f334b-110">그러나 Windows 클라이언트 또는 Windows 개발 환경에서 HDInsight로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-110">However, you can work with HDInsight from a Windows client or Windows development environment.</span></span>

## <a name="use-powershell-for-deployment-and-management-tasks"></a><span data-ttu-id="f334b-111">PowerShell을 사용하여 배포 및 관리 작업</span><span class="sxs-lookup"><span data-stu-id="f334b-111">Use PowerShell for deployment and management tasks</span></span>
<span data-ttu-id="f334b-112">Azure PowerShell은 Windows에서 HDInsight의 배포 및 관리 작업을 제어하고 자동화하는 데 사용할 수 있는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-112">Azure PowerShell is a scripting environment that you can use to control and automate deployment and management tasks in HDInsight from Windows.</span></span>

<span data-ttu-id="f334b-113">PowerShell로 수행할 수 있는 작업의 예:</span><span class="sxs-lookup"><span data-stu-id="f334b-113">Examples of tasks you can do with PowerShell:</span></span>

* [<span data-ttu-id="f334b-114">PowerShell을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f334b-114">Create clusters using PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="f334b-115">PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="f334b-115">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="f334b-116">PowerShell을 통한 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="f334b-116">Manage clusters with PowerShell</span></span>](hdinsight-administer-use-powershell.md)

<span data-ttu-id="f334b-117">[Azure Powershell 설치 및 구성](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 단계에 따라 최신 버전을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-117">Follow steps to [install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to get the latest version.</span></span> <span data-ttu-id="f334b-118">Azure Resource Manager용 새로운 cmdlet을 사용하도록 수정해야 하는 스크립트가 있는 경우 [HDInsight 클러스터에 대한 Azure Resource Manager 기반 개발 도구에 마이그레이션](hdinsight-hadoop-development-using-azure-resource-manager.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f334b-118">If you have scripts that need to be modified to use the new cmdlets for Azure Resource Manager, see [Migrate to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <a name="utilities-you-can-run-in-a-browser"></a><span data-ttu-id="f334b-119">브라우저에서 실행할 수 있는 유틸리티</span><span class="sxs-lookup"><span data-stu-id="f334b-119">Utilities you can run in a browser</span></span>
<span data-ttu-id="f334b-120">다음 유틸리티는 브라우저에서 실행되는 웹 UI가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-120">The following utilities have a web UI that runs in a browser:</span></span>
* <span data-ttu-id="f334b-121">**[Azure Cloud Shell(미리 보기)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**은 브라우저 및 Azure Portal 내에서 실행되는 대화형 명령줄 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-121">**[Azure Cloud Shell (preview)](https://docs.microsoft.com/azure/cloud-shell/quickstart)** is an interactive, command-line shell that runs in your browser and from within the Azure portal.</span></span>
* <span data-ttu-id="f334b-122">**[Ambari 웹 UI](hdinsight-hadoop-manage-ambari.md)**는 다음과 같은 다양한 종류의 작업을 관리하는 데 사용할 수 있으며 Azure Portal에서 사용 가능한 관리 및 모니터링 유틸리티입니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** is a management and monitoring utility available in the Azure portal that can be used to manage different kinds of jobs, such as:</span></span>
    * [<span data-ttu-id="f334b-123">REST API로 Ambari 사용</span><span class="sxs-lookup"><span data-stu-id="f334b-123">Use Ambari with the REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [<span data-ttu-id="f334b-124">Ambari에서 Hive 보기</span><span class="sxs-lookup"><span data-stu-id="f334b-124">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
    * [<span data-ttu-id="f334b-125">Ambari에서 Tez 보기</span><span class="sxs-lookup"><span data-stu-id="f334b-125">Tez View in Ambari</span></span>](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a><span data-ttu-id="f334b-126">Visual Studio용 Data Lake(Hadoop) 도구</span><span class="sxs-lookup"><span data-stu-id="f334b-126">Data Lake (Hadoop) Tools for Visual Studio</span></span>
<span data-ttu-id="f334b-127">Visual Studio용 Data Lake 도구를 사용하여 Storm 토폴로지를 배포 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-127">Use Data Lake Tools for Visual Studio to deploy and manage Storm topologies.</span></span> <span data-ttu-id="f334b-128">Data Lake 도구는 또한 Visual Studio와 함께 C# Storm 토폴로지를 개발할 수 있는 SCP.NET SDK를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-128">Data Lake Tools also installs the SCP.NET SDK, which allows you to develop C# Storm topologies with Visual Studio.</span></span>

<span data-ttu-id="f334b-129">다음 예제를 진행하기 전에 [Visual Studio용 Data Lake 도구를 설치 및 시도](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-129">Before you go to the following examples, [install and try Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span> 

<span data-ttu-id="f334b-130">다음은 Visual Studio용 Data Lake 도구와 Visual Studio를 사용할 수 있는 작업 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-130">Examples of tasks you can do with Visual Studio and Data Lake Tools for Visual Studio:</span></span>
* [<span data-ttu-id="f334b-131">Visual Studio에서 Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="f334b-131">Deploy and manage Storm topologies from Visual Studio</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
* <span data-ttu-id="f334b-132">[Visual Studio를 사용하여 Storm용 C# 토폴로지를 개발합니다](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f334b-132">[Develop C# topologies for Storm using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span> <span data-ttu-id="f334b-133">비트에는 Azure Cosmos DB 및 SQL Database와 같은 데이터베이스에 연결할 수 있는 Storm 토폴로지를 위한 예제 템플릿이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-133">The bits include example templates for Storm topologies you can connect to databases, such as Azure Cosmos DB and SQL Database.</span></span>

## <a name="visual-studio-and-the-net-sdk"></a><span data-ttu-id="f334b-134">Visual Studio 및 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f334b-134">Visual Studio and the .NET SDK</span></span> 

<span data-ttu-id="f334b-135">.NET SDK와 함께 Visual Studio를 사용하여 클러스터를 관리하고 빅 데이터 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-135">You can use Visual Studio with the .NET SDK to manage clusters and develop big data applications.</span></span> <span data-ttu-id="f334b-136">다음 작업에 대해 다른 IDE를 사용할 수 있으나 예제는 Visual Studio에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-136">You can use other IDEs for the following tasks, but examples are shown in Visual Studio.</span></span>

<span data-ttu-id="f334b-137">Visual Studio에서 .NET SDK와 함께 수행할 수 있는 작업의 예:</span><span class="sxs-lookup"><span data-stu-id="f334b-137">Examples of tasks you can do with the .NET SDK in Visual Studio:</span></span>
* [<span data-ttu-id="f334b-138">.NET Framework 응용 프로그램에서 클러스터 만들기 및 HDInsight 작업</span><span class="sxs-lookup"><span data-stu-id="f334b-138">Create clusters and work in HDInsight from a .NET Framework application</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [<span data-ttu-id="f334b-139">.NET SDK를 사용한 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="f334b-139">Run Hive queries using the .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="f334b-140">Hadoop에서 Hive 및 Pig 스트리밍과 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="f334b-140">Use C# user-defined functions with Hive and Pig streaming on Hadoop</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> <span data-ttu-id="f334b-141">팁 .NET 솔루션을 Windows 기반 HDInsight 클러스터와 함께 실행하는 경우 Linux 기반 클러스터로의 마이그레이션을 계획하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-141">TIP If you're running .NET solutions with Windows-based HDInsight clusters, it's a good time to plan a migration to Linux-based clusters.</span></span> <span data-ttu-id="f334b-142">자세한 내용은 [Windows 기반 HDInsight용 .NET 솔루션을 Linux 기반 HDInsight로 마이그레이션](hdinsight-hadoop-migrate-dotnet-to-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f334b-142">For more information, see [Migrate .NET solution for Windows-based HDInsight to Linux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a><span data-ttu-id="f334b-143">Spark 클러스터에 대한 Intellij IDEA 및 Eclipse IDE</span><span class="sxs-lookup"><span data-stu-id="f334b-143">Intellij IDEA and Eclipse IDE for Spark clusters</span></span>
<span data-ttu-id="f334b-144">[Intellij IDEA](https://www.jetbrains.com/idea/download) 및 [Eclipse IDE](https://www.eclipse.org/downloads/)는 다음에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-144">Both [Intellij IDEA](https://www.jetbrains.com/idea/download) and the [Eclipse IDE](https://www.eclipse.org/downloads/) can be used to:</span></span>
* <span data-ttu-id="f334b-145">HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-145">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="f334b-146">Spark 클러스터 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-146">Access Spark cluster resources.</span></span>
* <span data-ttu-id="f334b-147">Scala Spark 응용 프로그램을 로컬로 개발 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-147">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="f334b-148">다음 문서에 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-148">These articles show how:</span></span> 
* <span data-ttu-id="f334b-149">Intellij IDEA: [Intellij용 Azure 도구 키트 플러그 인 및 Scala SDK를 사용하여 Spark 응용 프로그램 만들기.](hdinsight-apache-spark-intellij-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="f334b-149">Intellij IDEA: [Create Spark applications using the Azure Toolkit for Intellij plug-in and the Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)</span></span>
* <span data-ttu-id="f334b-150">Eclipse IDE 또는 Eclipse용 Scala IDE: [Spark 응용 프로그램 및 Eclipse용 Azure 도구 키트 만들기](hdinsight-apache-spark-eclipse-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="f334b-150">Eclipse IDE or Scala IDE for Eclipse: [Create Spark applications and the Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span></span> 


## <a name="notebooks-on-spark-for-data-scientists"></a><span data-ttu-id="f334b-151">데이터 과학자들을 위한 Spark의 Notebook</span><span class="sxs-lookup"><span data-stu-id="f334b-151">Notebooks on Spark for data scientists</span></span> 
<span data-ttu-id="f334b-152">HDInsight의 Apache Spark 클러스터는 Jupyter Notebook과 함께 사용할 수 있는 Zeppelin Notebook 및 커널을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-152">Apache Spark clusters in HDInsight include Zeppelin notebooks and kernels that can be used with Jupyter notebooks.</span></span> 

* [<span data-ttu-id="f334b-153">Spark 클러스터에서 Jupyter Notebook과 함께 커널을 사용하여 Spark 응용 프로그램을 테스트하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="f334b-153">Learn how to use kernels on Spark clusters with Jupyter notebooks to test Spark applications</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="f334b-154">Spark 클러스터에서 Zeppelin Notebook을 사용하여 Spark 작업을 실행하는 방법 알아보기</span><span class="sxs-lookup"><span data-stu-id="f334b-154">Learn how to use Zeppelin notebooks on Spark clusters to run Spark jobs</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a><span data-ttu-id="f334b-155">Windows에서 Linux 기반 도구 및 기술 실행</span><span class="sxs-lookup"><span data-stu-id="f334b-155">Run Linux-based tools and technologies on Windows</span></span>

<span data-ttu-id="f334b-156">Linux에서만 사용 가능한 도구 또는 기술을 사용해야 하는 상황이 발생한 경우 다음 옵션을 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-156">If you encounter a situation where you must use a tool or technology that is only available on Linux, consider the following options:</span></span>

* <span data-ttu-id="f334b-157">**Windows 10의 Bash(베타)**는 Windows에서 Linux 하위 시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-157">**Bash (beta) on Windows 10** provides a Linux subsystem on Windows.</span></span> <span data-ttu-id="f334b-158">Bash를 사용하면 전용 Linux 설치를 유지하지 않고도 Linux 유틸리티를 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-158">Bash allows you to directly run Linux utilities without having to maintain a dedicated Linux installation.</span></span> [<span data-ttu-id="f334b-159">Bash 베타를 Windows 10에서 설치 및 실행</span><span class="sxs-lookup"><span data-stu-id="f334b-159">Install and run the Bash beta on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/install_guide)
* <span data-ttu-id="f334b-160">**Windows용 Docker**는 대부분의 Linux 기반 도구에 대한 액세스를 제공하며 Windows에서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-160">**Docker for Windows** provides access to many Linux-based tools, and can be run directly from Windows.</span></span> <span data-ttu-id="f334b-161">예를 들어, Docker를 사용하여 Hive에 대한 Beeline 클라이언트를 Windows에서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-161">For example, you can use Docker to run the Beeline client for Hive directly from Windows.</span></span> <span data-ttu-id="f334b-162">또한 Docker를 사용하여 로컬 Jupyter Notebook을 실행하고 HDInsight의 Spark에 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-162">You can also use Docker to run a local Jupyter notebook and remotely connect to Spark on HDInsight.</span></span> [<span data-ttu-id="f334b-163">Windows용 Docker 시작</span><span class="sxs-lookup"><span data-stu-id="f334b-163">Get started with Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/)
* <span data-ttu-id="f334b-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)**을 사용하면 그래픽 방식으로 SSH 연결을 통해 클러스터 파일 시스템을 찾아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f334b-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** allows you to graphically browse the cluster file system over an SSH connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f334b-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="f334b-165">Next steps</span></span>
<span data-ttu-id="f334b-166">Linux 기반 클러스터에서 작업하는 데 익숙하지 않은 경우 다음 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f334b-166">If you're new to working in Linux-based clusters, see the follow articles:</span></span>
* [<span data-ttu-id="f334b-167">Hadoop, Kafka, Spark 또는 다른 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="f334b-167">Set up Hadoop, Kafka, Spark, or other clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="f334b-168">Linux의 HDInsight 클러스터에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="f334b-168">Tips for HDInsight clusters on Linux</span></span>](hdinsight-hadoop-linux-information.md)