---
title: "PowerShell를 사용하여 Hadoop 클러스터 만들기 - Azure HDInsight | Microsoft Docs"
description: "Azure PowerShell을 사용하여 Linux 기반 HDInsight에서 Hadoop, HBase, Storm 또는 Spark 클러스터를 만드는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="1ea4d-103">Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="1ea4d-104">Azure PowerShell은 Microsoft Azure에서 작업의 배포와 관리를 제어 및 자동화하기 위해 사용할 수 있는 강력한 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="1ea4d-105">이 문서에서는 Azure PowerShell을 사용하여 Linux 기반 HDInsight 클러스터를 만드는 방법에 대한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="1ea4d-106">또한 예제 스크립트도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="1ea4d-107">Azure PowerShell은 Windows 클라이언트에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="1ea4d-108">Linux, Unix 또는 Mac OS X 클라이언트를 사용하는 경우 Azure CLI를 사용하여 클러스터 만들기에 대한 정보에 대해 [Azure CLI를 사용하여 Linux 기반 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-cli.md) 를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ea4d-109">필수 조건</span><span class="sxs-lookup"><span data-stu-id="1ea4d-109">Prerequisites</span></span>
<span data-ttu-id="1ea4d-110">이 절차를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="1ea4d-111">Azure 구독.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-111">An Azure subscription.</span></span> <span data-ttu-id="1ea4d-112">[Azure 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="1ea4d-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1ea4d-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="1ea4d-114">Azure Service Manager를 사용하여 HDInsight 리소스를 관리하는 Azure PowerShell 지원은 더 이상 **지원되지 않고** 2017년 1월 1일에 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1ea4d-115">이 문서의 단계에서는 Azure Resource Manager로 작동하는 새 HDInsight cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1ea4d-116">[Azure PowerShell 설치 및 구성](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 단계를 수행하여 최신 버전의 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="1ea4d-117">Azure Resource Manager로 작동하는 새로운 cmdlet을 사용하도록 수정해야 하는 스크립트가 있는 경우 자세한 내용은 [HDInsight 클러스터에 대한 Azure Resource Manager 기반 개발 도구에 마이그레이션](hdinsight-hadoop-development-using-azure-resource-manager.md) 을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="1ea4d-118">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1ea4d-119">Azure PowerShell을 사용하여 HDInsight 클러스터를 만들려면 다음 절차를 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="1ea4d-120">Azure 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-120">Create an Azure resource group</span></span>
* <span data-ttu-id="1ea4d-121">Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="1ea4d-122">Azure Blob 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="1ea4d-123">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="1ea4d-124">다음 스크립트는 새 클러스터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="1ea4d-125">[!code-powershell[기본](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="1ea4d-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="1ea4d-126">클러스터 로그인에 대해 지정한 값은 클러스터의 Hadoop 사용자 계정을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="1ea4d-127">이 계정을 사용하여 웹 UI 또는 REST API 등의 클러스터에서 호스팅된 서비스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="1ea4d-128">SSH 사용자에 대해 지정한 값은 클러스터의 SSH 사용자를 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="1ea4d-129">이 계정을 사용하여 클러스터에서 원격 SSH 세션을 시작하고 작업을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="1ea4d-130">자세한 내용은 [HDInsight와 함께 SSH 사용](hdinsight-hadoop-linux-use-ssh-unix.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1ea4d-131">클러스터를 생성할 때 또는 생성 후 클러스터를 확장할 때 32개 이상의 작업자 노드를 사용하려는 경우 최소한 8개의 노드와 14GB RAM으로 헤드 노드의 크기를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="1ea4d-132">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="1ea4d-133">클러스터를 만드는 데 최대 20분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="1ea4d-134">클러스터 만들기: 구성 개체</span><span class="sxs-lookup"><span data-stu-id="1ea4d-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="1ea4d-135">또한 `New-AzureRmHDInsightClusterConfig` cmdlet을 사용하여 HDInsight 구성 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="1ea4d-136">그런 다음 이 구성 개체를 수정하여 클러스터에 대한 추가 구성 옵션을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="1ea4d-137">마지막으로 `New-AzureRmHDInsightCluster` cmdlet의 `-Config` 매개 변수를 사용하여 구성을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="1ea4d-138">다음 스크립트는 HDInsight 클러스터 유형에 R Server를 구성하기 위해 구성 개체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="1ea4d-139">이 구성은 에지 노드, RStudio, 추가 저장소 계정을 활성화합니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="1ea4d-140">[!code-powershell[기본](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="1ea4d-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="1ea4d-141">HDInsight 클러스터와 다른 위치에서는 저장소 계정을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="1ea4d-142">이 예제를 사용할 경우 서버와 동일한 위치에 추가 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="1ea4d-143">클러스터 사용자 지정</span><span class="sxs-lookup"><span data-stu-id="1ea4d-143">Customize clusters</span></span>

* <span data-ttu-id="1ea4d-144">[부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="1ea4d-145">[스크립트 동작을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="1ea4d-146">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="1ea4d-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="1ea4d-147">문제 해결</span><span class="sxs-lookup"><span data-stu-id="1ea4d-147">Troubleshoot</span></span>

<span data-ttu-id="1ea4d-148">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ea4d-149">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1ea4d-149">Next steps</span></span>

<span data-ttu-id="1ea4d-150">HDInsight 클러스터를 성공적으로 만들었으므로 다음 리소스를 사용하여 클러스터 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="1ea4d-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="1ea4d-151">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="1ea4d-151">Hadoop clusters</span></span>

* [<span data-ttu-id="1ea4d-152">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="1ea4d-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1ea4d-153">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="1ea4d-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1ea4d-154">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="1ea4d-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="1ea4d-155">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="1ea4d-155">HBase clusters</span></span>

* [<span data-ttu-id="1ea4d-156">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="1ea4d-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="1ea4d-157">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="1ea4d-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="1ea4d-158">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="1ea4d-158">Storm clusters</span></span>

* [<span data-ttu-id="1ea4d-159">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="1ea4d-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="1ea4d-160">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="1ea4d-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="1ea4d-161">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="1ea4d-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="1ea4d-162">Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="1ea4d-162">Spark clusters</span></span>

* [<span data-ttu-id="1ea4d-163">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="1ea4d-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1ea4d-164">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="1ea4d-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="1ea4d-165">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="1ea4d-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1ea4d-166">기계 학습과 Spark: 음식 검사 결과를 예측하는 데 HDInsight의 Spark 사용</span><span class="sxs-lookup"><span data-stu-id="1ea4d-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="1ea4d-167">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="1ea4d-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

