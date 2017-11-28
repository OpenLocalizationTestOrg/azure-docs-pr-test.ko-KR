---
title: "aaaCreate Hadoop 클러스터 PowerShell-Azure HDInsight를 사용 하 여 | Microsoft Docs"
description: "어떻게 toocreate Hadoop, HBase, 스톰, 또는 Spark 클러스터 Linux에서 HDInsight에 대 한 Azure PowerShell을 사용 하 여에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="a9247-103">Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a9247-104">Azure PowerShell은 toocontrol를 사용 하 고 Microsoft Azure에서 작업의 hello 배포 및 관리를 자동화할 수 있는 강력한 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="a9247-105">이 문서는 Azure PowerShell을 사용 하 여 toocreate Linux 기반 HDInsight 클러스터 하는 방법에 대 한 정보를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="a9247-106">또한 예제 스크립트도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="a9247-107">Azure PowerShell은 Windows 클라이언트에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="a9247-108">Linux, Unix, 또는 Mac OS X 클라이언트를 사용 하는 경우 참조 [Azure CLI를 사용 하 여 Linux 기반 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md) hello Azure CLI toocreate 클러스터 사용에 대 한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9247-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a9247-109">Prerequisites</span></span>
<span data-ttu-id="a9247-110">이 절차를 시작 하기 전에 hello 다음이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="a9247-111">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="a9247-111">An Azure subscription.</span></span> <span data-ttu-id="a9247-112">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9247-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="a9247-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9247-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="a9247-114">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="a9247-115">Azure 리소스 관리자와 함께 작동 하는이 문서 사용 hello 새 HDInsight cmdlet의 hello 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="a9247-116">Hello 단계에 따라 [Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello 최신 버전의 Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a9247-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="a9247-117">해당 필요 toobe Azure 리소스 관리자와 함께 작동 하는 toouse hello 새로운 cmdlet 수정 스크립트가 있는 경우, 참조 [HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구](hdinsight-hadoop-development-using-azure-resource-manager.md) 자세한 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="a9247-118">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="a9247-119">Azure PowerShell을 사용 하 여 HDInsight 클러스터 toocreate hello 다음 절차를 완료 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="a9247-120">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-120">Create an Azure resource group</span></span>
* <span data-ttu-id="a9247-121">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="a9247-122">Azure Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="a9247-123">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="a9247-124">hello 다음 스크립트에서는 방법을 toocreate 새 클러스터:</span><span class="sxs-lookup"><span data-stu-id="a9247-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="a9247-125">hello 클러스터 로그인에 대해 지정 하는 hello 값은 사용 되는 toocreate hello hello 클러스터에 대 한 Hadoop 사용자 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="a9247-126">이 계정 tooconnect tooservices 웹 Ui 또는 REST Api와 같은 hello 클러스터에서 호스트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="a9247-127">hello SSH 사용자에 대해 지정 하는 hello 값은 hello 클러스터에 대 한 사용 되는 toocreate hello SSH 사용자입니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="a9247-128">이 사용 하 여 원격 SSH 세션 toostart hello 클러스터에서 계정 및 작업을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="a9247-129">자세한 내용은 참조 hello [SSH HDInsight를 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서.</span><span class="sxs-lookup"><span data-stu-id="a9247-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a9247-130">(클러스터를 만들 때 또는 hello 크기 조정 하 여 클러스터를 만든 후) 32 개 이상의 작업자 노드 toouse 하려는 경우에 적어도 8 코어, 14GB ram와 헤드 노드 크기를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="a9247-131">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9247-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="a9247-132">클러스터를 too20 분 toocreate 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="a9247-133">클러스터 만들기: 구성 개체</span><span class="sxs-lookup"><span data-stu-id="a9247-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="a9247-134">또한 `New-AzureRmHDInsightClusterConfig` cmdlet을 사용하여 HDInsight 구성 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="a9247-135">그런 다음 클러스터에 대해이 구성 개체 tooenable 추가 구성 옵션을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="a9247-136">마지막으로 hello를 사용 하 여 `-Config` hello의 매개 변수 `New-AzureRmHDInsightCluster` cmdlet toouse hello 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="a9247-137">hello 다음 스크립트는 구성 개체 tooconfigure를 R 서버에 만듭니다 HDInsight 클러스터 유형.</span><span class="sxs-lookup"><span data-stu-id="a9247-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="a9247-138">hello 구성을 통해 가장자리 노드, RStudio, 및 추가 저장소 계정 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="a9247-139">저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="a9247-140">이 예제를 사용할 때는 hello에 hello 추가 저장소 계정을 만들 hello 서버와 동일한 위치 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="a9247-141">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="a9247-141">Customize clusters</span></span>

* <span data-ttu-id="a9247-142">[부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9247-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="a9247-143">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9247-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="a9247-144">Hello 클러스터를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="a9247-145">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a9247-145">Troubleshoot</span></span>

<span data-ttu-id="a9247-146">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a9247-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9247-147">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a9247-147">Next steps</span></span>

<span data-ttu-id="a9247-148">HDInsight 클러스터를 성공적으로 만든 리소스 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="a9247-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="a9247-149">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="a9247-149">Hadoop clusters</span></span>

* [<span data-ttu-id="a9247-150">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="a9247-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a9247-151">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="a9247-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a9247-152">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="a9247-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="a9247-153">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="a9247-153">HBase clusters</span></span>

* [<span data-ttu-id="a9247-154">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="a9247-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="a9247-155">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="a9247-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="a9247-156">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="a9247-156">Storm clusters</span></span>

* [<span data-ttu-id="a9247-157">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="a9247-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a9247-158">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="a9247-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="a9247-159">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="a9247-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="a9247-160">Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="a9247-160">Spark clusters</span></span>

* [<span data-ttu-id="a9247-161">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="a9247-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a9247-162">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="a9247-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="a9247-163">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="a9247-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a9247-164">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="a9247-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a9247-165">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="a9247-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

