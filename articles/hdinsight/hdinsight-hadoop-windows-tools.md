---
title: "Azure HDInsight의 Hadoop 사용 하 여 Windows PC를 aaaUse | Microsoft Docs"
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
ms.openlocfilehash: 7c93f16e93349c0b8fb1abd55320c2c172b93aa9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="work-in-hello-hadoop-ecosystem-on-hdinsight-from-a-windows-pc"></a><span data-ttu-id="118e3-106">Windows PC에서 HDInsight의 Hadoop 생태계 hello에서 작업</span><span class="sxs-lookup"><span data-stu-id="118e3-106">Work in hello Hadoop ecosystem on HDInsight from a Windows PC</span></span>

<span data-ttu-id="118e3-107">HDInsight의 Hadoop 생태계 hello에서에서 작업 하기 위한 개발 및 hello Windows PC에 대 한 관리 옵션에 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-107">Learn about development and management options on hello Windows PC for working in hello Hadoop ecosystem on HDInsight.</span></span> 

<span data-ttu-id="118e3-108">HDInsight는 Apache Hadoop 및 Hadoop 구성 요소, Linux에서 개발된 오픈 소스 기술을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-108">HDInsight is based on Apache Hadoop and Hadoop components, open-source technologies developed on Linux.</span></span> <span data-ttu-id="118e3-109">HDInsight 버전 3.4 이상 hello hello 클러스터에 대 한 운영 체제를 기본으로 hello Ubuntu Linux 배포를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-109">HDInsight version 3.4 and higher uses hello Ubuntu Linux distribution as hello underlying OS for hello cluster.</span></span> <span data-ttu-id="118e3-110">그러나 Windows 클라이언트 또는 Windows 개발 환경에서 HDInsight로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-110">However, you can work with HDInsight from a Windows client or Windows development environment.</span></span>

## <a name="use-powershell-for-deployment-and-management-tasks"></a><span data-ttu-id="118e3-111">PowerShell을 사용하여 배포 및 관리 작업</span><span class="sxs-lookup"><span data-stu-id="118e3-111">Use PowerShell for deployment and management tasks</span></span>
<span data-ttu-id="118e3-112">Azure PowerShell은 toocontrol를 사용할 수 있으며 Windows에서 HDInsight의 배포 및 관리 작업을 자동화 하는 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-112">Azure PowerShell is a scripting environment that you can use toocontrol and automate deployment and management tasks in HDInsight from Windows.</span></span>

<span data-ttu-id="118e3-113">PowerShell로 수행할 수 있는 작업의 예:</span><span class="sxs-lookup"><span data-stu-id="118e3-113">Examples of tasks you can do with PowerShell:</span></span>

* [<span data-ttu-id="118e3-114">PowerShell을 사용하여 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="118e3-114">Create clusters using PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="118e3-115">PowerShell을 사용하여 Hive 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="118e3-115">Run Hive queries using PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="118e3-116">PowerShell을 통한 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="118e3-116">Manage clusters with PowerShell</span></span>](hdinsight-administer-use-powershell.md)

<span data-ttu-id="118e3-117">다음과 같이 너무[Azure Powershell 설치 및 구성](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello 최신 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-117">Follow steps too[install and configure Azure Powershell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooget hello latest version.</span></span> <span data-ttu-id="118e3-118">Azure 리소스 관리자에 대 한 수정 toobe toouse hello에 대 한 새로운 cmdlet을 필요로 하는 스크립트를 사용 하도록 설정한 경우 참조 [HDInsight 클러스터에 대 한 리소스 관리자 기반 개발 도구 tooAzure 마이그레이션할](hdinsight-hadoop-development-using-azure-resource-manager.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-118">If you have scripts that need toobe modified toouse hello new cmdlets for Azure Resource Manager, see [Migrate tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <a name="utilities-you-can-run-in-a-browser"></a><span data-ttu-id="118e3-119">브라우저에서 실행할 수 있는 유틸리티</span><span class="sxs-lookup"><span data-stu-id="118e3-119">Utilities you can run in a browser</span></span>
<span data-ttu-id="118e3-120">hello 다음 유틸리티는 웹 브라우저에서 실행 되는 UI:</span><span class="sxs-lookup"><span data-stu-id="118e3-120">hello following utilities have a web UI that runs in a browser:</span></span>
* <span data-ttu-id="118e3-121">**[Azure 클라우드 셸 (미리 보기)](https://docs.microsoft.com/azure/cloud-shell/quickstart)**  브라우저에서 실행 되는 대화형 명령줄 셸인 및 hello Azure 포털 내에서.</span><span class="sxs-lookup"><span data-stu-id="118e3-121">**[Azure Cloud Shell (preview)](https://docs.microsoft.com/azure/cloud-shell/quickstart)** is an interactive, command-line shell that runs in your browser and from within hello Azure portal.</span></span>
* <span data-ttu-id="118e3-122">**[Ambari 웹 UI](hdinsight-hadoop-manage-ambari.md)**  는 관리 및 모니터링 유틸리티 hello와 같은 사용된 toomanage 다양 한 종류의 작업을 수 있는 Azure 포털에서에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-122">**[Ambari Web UI](hdinsight-hadoop-manage-ambari.md)** is a management and monitoring utility available in hello Azure portal that can be used toomanage different kinds of jobs, such as:</span></span>
    * [<span data-ttu-id="118e3-123">Ambari를 사용 하 여 hello REST API로</span><span class="sxs-lookup"><span data-stu-id="118e3-123">Use Ambari with hello REST API</span></span>](hdinsight-hadoop-manage-ambari-rest-api.md)
    * [<span data-ttu-id="118e3-124">Ambari에서 Hive 보기</span><span class="sxs-lookup"><span data-stu-id="118e3-124">Hive View in Ambari</span></span>](hdinsight-hadoop-use-hive-ambari-view.md)
    * [<span data-ttu-id="118e3-125">Ambari에서 Tez 보기</span><span class="sxs-lookup"><span data-stu-id="118e3-125">Tez View in Ambari</span></span>](hdinsight-debug-ambari-tez-view.md)

## <a name="data-lake-hadoop-tools-for-visual-studio"></a><span data-ttu-id="118e3-126">Visual Studio용 Data Lake(Hadoop) 도구</span><span class="sxs-lookup"><span data-stu-id="118e3-126">Data Lake (Hadoop) Tools for Visual Studio</span></span>
<span data-ttu-id="118e3-127">Visual Studio toodeploy에 대 한 데이터 레이크 도구를 사용 하 고 스톰 토폴로지를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-127">Use Data Lake Tools for Visual Studio toodeploy and manage Storm topologies.</span></span> <span data-ttu-id="118e3-128">데이터 레이크 도구는 또한 hello Visual Studio와 함께 C# 스톰 토폴로지 toodevelop 있습니다 SCP.NET SDK를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-128">Data Lake Tools also installs hello SCP.NET SDK, which allows you toodevelop C# Storm topologies with Visual Studio.</span></span>

<span data-ttu-id="118e3-129">예제를 따르는 toohello를 진행 하기 전에 [설치 하 고 Visual Studio에 대 한 데이터 레이크 도구 시도](hdinsight-hadoop-visual-studio-tools-get-started.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-129">Before you go toohello following examples, [install and try Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span> 

<span data-ttu-id="118e3-130">다음은 Visual Studio용 Data Lake 도구와 Visual Studio를 사용할 수 있는 작업 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-130">Examples of tasks you can do with Visual Studio and Data Lake Tools for Visual Studio:</span></span>
* [<span data-ttu-id="118e3-131">Visual Studio에서 Storm 토폴로지 배포 및 관리</span><span class="sxs-lookup"><span data-stu-id="118e3-131">Deploy and manage Storm topologies from Visual Studio</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
* <span data-ttu-id="118e3-132">[Visual Studio를 사용하여 Storm용 C# 토폴로지를 개발합니다](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="118e3-132">[Develop C# topologies for Storm using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span> <span data-ttu-id="118e3-133">hello 비트 예제 서식 파일을 포함 스톰 토폴로지에 대 한 Azure Cosmos DB와 SQL 데이터베이스 같은 toodatabases를 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-133">hello bits include example templates for Storm topologies you can connect toodatabases, such as Azure Cosmos DB and SQL Database.</span></span>

## <a name="visual-studio-and-hello-net-sdk"></a><span data-ttu-id="118e3-134">Visual Studio 및.NET SDK hello</span><span class="sxs-lookup"><span data-stu-id="118e3-134">Visual Studio and hello .NET SDK</span></span> 

<span data-ttu-id="118e3-135">Visual Studio를 사용 하 여 hello.NET SDK toomanage 클러스터 수 있으며, 빅 데이터 응용 프로그램을 개발할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-135">You can use Visual Studio with hello .NET SDK toomanage clusters and develop big data applications.</span></span> <span data-ttu-id="118e3-136">작업을 수행 하는 hello에 대 한 기타 Ide를 사용할 수 있지만 Visual Studio에 예가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-136">You can use other IDEs for hello following tasks, but examples are shown in Visual Studio.</span></span>

<span data-ttu-id="118e3-137">Visual Studio에서.NET SDK hello로 수행할 수 있는 작업의 예:</span><span class="sxs-lookup"><span data-stu-id="118e3-137">Examples of tasks you can do with hello .NET SDK in Visual Studio:</span></span>
* [<span data-ttu-id="118e3-138">.NET Framework 응용 프로그램에서 클러스터 만들기 및 HDInsight 작업</span><span class="sxs-lookup"><span data-stu-id="118e3-138">Create clusters and work in HDInsight from a .NET Framework application</span></span>](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* [<span data-ttu-id="118e3-139">Hello.NET SDK를 사용 하는 하이브 쿼리를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-139">Run Hive queries using hello .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="118e3-140">Hadoop에서 Hive 및 Pig 스트리밍과 함께 C# 사용자 정의 함수 사용</span><span class="sxs-lookup"><span data-stu-id="118e3-140">Use C# user-defined functions with Hive and Pig streaming on Hadoop</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

> <span data-ttu-id="118e3-141">팁.NET 솔루션 Windows 기반 HDInsight 클러스터를 실행 중인 경우 좋은 시간 tooplan 마이그레이션 tooLinux 기반 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-141">TIP If you're running .NET solutions with Windows-based HDInsight clusters, it's a good time tooplan a migration tooLinux-based clusters.</span></span> <span data-ttu-id="118e3-142">자세한 내용은 참조 [Windows 기반 HDInsight에 대 한 마이그레이션.NET 솔루션 tooLinux 기반 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-142">For more information, see [Migrate .NET solution for Windows-based HDInsight tooLinux-based HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md).</span></span>

## <a name="intellij-idea-and-eclipse-ide-for-spark-clusters"></a><span data-ttu-id="118e3-143">Spark 클러스터에 대한 Intellij IDEA 및 Eclipse IDE</span><span class="sxs-lookup"><span data-stu-id="118e3-143">Intellij IDEA and Eclipse IDE for Spark clusters</span></span>
<span data-ttu-id="118e3-144">둘 다 [Intellij 아이디어](https://www.jetbrains.com/idea/download) 및 hello [Eclipse IDE](https://www.eclipse.org/downloads/) 에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-144">Both [Intellij IDEA](https://www.jetbrains.com/idea/download) and hello [Eclipse IDE](https://www.eclipse.org/downloads/) can be used to:</span></span>
* <span data-ttu-id="118e3-145">HDInsight Spark 클러스터에서 Scala Spark 응용 프로그램을 개발 및 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-145">Develop and submit a Scala Spark application on an HDInsight Spark cluster.</span></span>
* <span data-ttu-id="118e3-146">Spark 클러스터 리소스에 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-146">Access Spark cluster resources.</span></span>
* <span data-ttu-id="118e3-147">Scala Spark 응용 프로그램을 로컬로 개발 및 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-147">Develop and run a Scala Spark application locally.</span></span>

<span data-ttu-id="118e3-148">다음 문서에 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-148">These articles show how:</span></span> 
* <span data-ttu-id="118e3-149">Intellij 아이디어: [hello Intellij 플러그 인에 대 한 Azure 도구 키트 및 hello Scala SDK를 사용 하 여 만들기 Spark 응용 프로그램입니다.](hdinsight-apache-spark-intellij-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="118e3-149">Intellij IDEA: [Create Spark applications using hello Azure Toolkit for Intellij plug-in and hello Scala SDK.](hdinsight-apache-spark-intellij-tool-plugin.md)</span></span>
* <span data-ttu-id="118e3-150">Eclipse IDE 또는 Eclipse 용 Scala IDE: [Spark 만들 응용 프로그램 및 hello Eclipse 용 Azure 도구 키트](hdinsight-apache-spark-eclipse-tool-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="118e3-150">Eclipse IDE or Scala IDE for Eclipse: [Create Spark applications and hello Azure Toolkit for Eclipse](hdinsight-apache-spark-eclipse-tool-plugin.md)</span></span> 


## <a name="notebooks-on-spark-for-data-scientists"></a><span data-ttu-id="118e3-151">데이터 과학자들을 위한 Spark의 Notebook</span><span class="sxs-lookup"><span data-stu-id="118e3-151">Notebooks on Spark for data scientists</span></span> 
<span data-ttu-id="118e3-152">HDInsight의 Apache Spark 클러스터는 Jupyter Notebook과 함께 사용할 수 있는 Zeppelin Notebook 및 커널을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-152">Apache Spark clusters in HDInsight include Zeppelin notebooks and kernels that can be used with Jupyter notebooks.</span></span> 

* [<span data-ttu-id="118e3-153">Jupyter 노트북 tootest Spark 응용 프로그램과 toouse 커널 Spark에 클러스터 되는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="118e3-153">Learn how toouse kernels on Spark clusters with Jupyter notebooks tootest Spark applications</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="118e3-154">Spark에서 toouse 선을 전자 필기장 toorun Spark 작업을 클러스터 하는 방법에 대해 알아봅니다</span><span class="sxs-lookup"><span data-stu-id="118e3-154">Learn how toouse Zeppelin notebooks on Spark clusters toorun Spark jobs</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md) 


## <a name="run-linux-based-tools-and-technologies-on-windows"></a><span data-ttu-id="118e3-155">Windows에서 Linux 기반 도구 및 기술 실행</span><span class="sxs-lookup"><span data-stu-id="118e3-155">Run Linux-based tools and technologies on Windows</span></span>

<span data-ttu-id="118e3-156">도구 또는 Linux에서 사용할 수 있는 기술을 사용 해야 하는 상황이 발생 하는 경우 다음 옵션 hello를 고려해 야 합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-156">If you encounter a situation where you must use a tool or technology that is only available on Linux, consider hello following options:</span></span>

* <span data-ttu-id="118e3-157">**Windows 10의 Bash(베타)**는 Windows에서 Linux 하위 시스템을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-157">**Bash (beta) on Windows 10** provides a Linux subsystem on Windows.</span></span> <span data-ttu-id="118e3-158">Bash toodirectly를 toomaintain 전용된 Linux 설치 필요 없이 Linux 유틸리티를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-158">Bash allows you toodirectly run Linux utilities without having toomaintain a dedicated Linux installation.</span></span> [<span data-ttu-id="118e3-159">설치 하 고 Windows 10에서 hello Bash 베타 실행</span><span class="sxs-lookup"><span data-stu-id="118e3-159">Install and run hello Bash beta on Windows 10</span></span>](https://msdn.microsoft.com/commandline/wsl/install_guide)
* <span data-ttu-id="118e3-160">**Windows 용 docker** toomany Linux 기반 도구 액세스를 제공 하며 Windows에서 직접 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-160">**Docker for Windows** provides access toomany Linux-based tools, and can be run directly from Windows.</span></span> <span data-ttu-id="118e3-161">예를 들어 Windows에서 직접 하이브에 대 한 Docker toorun hello Beeline 클라이언트를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-161">For example, you can use Docker toorun hello Beeline client for Hive directly from Windows.</span></span> <span data-ttu-id="118e3-162">또한 Docker toorun 로컬 Jupyter 노트북을 사용 하 여 수 있으며 원격으로 연결 하는 HDInsight의 tooSpark 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-162">You can also use Docker toorun a local Jupyter notebook and remotely connect tooSpark on HDInsight.</span></span> [<span data-ttu-id="118e3-163">Windows용 Docker 시작</span><span class="sxs-lookup"><span data-stu-id="118e3-163">Get started with Docker for Windows</span></span>](https://docs.docker.com/docker-for-windows/)
* <span data-ttu-id="118e3-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)**  SSH 연결을 통해 toographically 찾아보기 hello 클러스터 파일 시스템 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-164">**[MobaXTerm](http://mobaxterm.mobatek.net/)** allows you toographically browse hello cluster file system over an SSH connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="118e3-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="118e3-165">Next steps</span></span>
<span data-ttu-id="118e3-166">Linux 기반 클러스터에서 새 tooworking 인 경우 참조 hello 문서를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="118e3-166">If you're new tooworking in Linux-based clusters, see hello follow articles:</span></span>
* [<span data-ttu-id="118e3-167">Hadoop, Kafka, Spark 또는 다른 클러스터 설정</span><span class="sxs-lookup"><span data-stu-id="118e3-167">Set up Hadoop, Kafka, Spark, or other clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="118e3-168">Linux의 HDInsight 클러스터에 대한 팁</span><span class="sxs-lookup"><span data-stu-id="118e3-168">Tips for HDInsight clusters on Linux</span></span>](hdinsight-hadoop-linux-information.md)