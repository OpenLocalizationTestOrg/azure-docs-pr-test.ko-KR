---
title: "명령줄을 사용하여 Hadoop 클러스터 만들기 - Azure HDInsight | Microsoft Docs"
description: "플랫폼 간 Azure CLI 1.0을 사용하여 HDInsight 클러스터를 만드는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="00a67-103">Azure CLI를 사용하여 HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="00a67-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="00a67-104">이 문서의 단계는 Azure CLI 1.0을 사용하여 HDInsight 3.5 클러스터 만들기 과정을 연습합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00a67-105">Linux는 HDInsight 버전 3.4 이상에서 사용되는 유일한 운영 체제입니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="00a67-106">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00a67-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="00a67-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="00a67-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="00a67-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="00a67-108">**An Azure subscription**.</span></span> <span data-ttu-id="00a67-109">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00a67-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="00a67-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="00a67-110">**Azure CLI**.</span></span> <span data-ttu-id="00a67-111">이 문서의 단계는 Azure CLI 버전 0.10.14에서 마지막으로 테스트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="00a67-112">이 문서의 단계는 Azure CLI 2.0에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="00a67-113">Azure CLI 2.0은 HDInsight 클러스터 만들기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="00a67-114">Azure 구독에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="00a67-115">[Azure CLI(Azure 명령줄 인터페이스)에서 Azure 구독에 연결](../xplat-cli-connect.md) 에서 설명된 단계에 따라 **login** 메서드를 사용하여 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="00a67-116">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="00a67-116">Create a cluster</span></span>

<span data-ttu-id="00a67-117">PowerShell 또는 Bash 등의 명령줄에서 다음 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="00a67-118">다음 명령을 사용하여 Azure 구독에 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="00a67-119">사용자 이름 및 암호를 제공하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="00a67-120">여러 Azure 구독이 있는 경우 `azure account set <subscriptionname>` 을 사용하여 Azure CLI 명령이 사용할 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="00a67-121">다음 명령을 사용하여 Azure 리소스 관리자 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="00a67-122">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-122">Create a resource group.</span></span> <span data-ttu-id="00a67-123">이 리소스 그룹에는 HDInsight 클러스터 및 연결된 저장소 계정이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="00a67-124">`groupname`을 그룹의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="00a67-125">`location`을 그룹을 만들 지리적 지역으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="00a67-126">유효한 위치 목록을 위해 `azure location list` 명령을 사용한 다음 `Name` 열의 위치 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="00a67-127">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-127">Create a storage account.</span></span> <span data-ttu-id="00a67-128">이 저장소 계정은 HDInsight 클러스터에 대한 기본 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="00a67-129">`groupname`을 이전 단계에서 만든 그룹의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="00a67-130">`location`을 이전 단계에서 사용된 동일한 위치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="00a67-131">`storagename`을 저장소 계정의 고유한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="00a67-132">이 명령에서 사용된 매개 변수에 대한 자세한 내용을 보려면 `azure storage account create -h`를 사용하여 이 명령에 대한 도움말을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="00a67-133">저장소 계정에 액세스하는 데 사용된 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="00a67-134">`groupname`을 리소스 그룹 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="00a67-135">`storagename`을 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="00a67-136">반환된 데이터에서 `key1`의 `key` 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="00a67-137">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="00a67-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="00a67-138">`groupname`을 리소스 그룹 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="00a67-139">`Hadoop`을 만들려는 클러스터 유형으로 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="00a67-140">예를 들어 `Hadoop`, `HBase`, `Kafka`, `Spark` 또는 `Storm`입니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="00a67-141">HDInsight 클러스터는 워크로드 또는 클러스터에 대한 튜닝 기술에 해당하는 다양한 형식을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="00a67-142">하나의 클러스터에서 Storm 및 HBase 등의 여러 유형을 결합하는 클러스터를 만들기 위해 지원되는 메서드가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="00a67-143">`location`을 이전 단계에서 사용된 동일한 위치로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="00a67-144">`storagename`을 저장소 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="00a67-145">`storagekey`를 이전 단계에서 얻은 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="00a67-146">`--defaultStorageContainer` 매개 변수의 경우 클러스터에 사용하는 것과 같은 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="00a67-147">`admin` 및 `httppassword`를 HTTPS를 통해 클러스터에 액세스할 때 사용할 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="00a67-148">`sshuser` 및 `sshuserpassword`를 SSH를 통해 클러스터에 액세스할 때 사용할 사용자 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="00a67-149">이 예제에서는 2개의 작업자 노드를 사용하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="00a67-150">클러스터를 만든 후 크기 조정 작업을 수행하여 작업자 노드 수를 변경할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="00a67-151">사용하려는 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="00a67-152">클러스터를 만드는 동안 `--headNodeSize` 매개 변수를 사용하여 헤드 노드 크기를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="00a67-153">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00a67-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="00a67-154">클러스터 생성 프로세스를 완료하는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="00a67-155">일반적으로 약 15분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="00a67-156">문제 해결</span><span class="sxs-lookup"><span data-stu-id="00a67-156">Troubleshoot</span></span>

<span data-ttu-id="00a67-157">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="00a67-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00a67-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="00a67-158">Next steps</span></span>

<span data-ttu-id="00a67-159">Azure CLI를 사용하여 HDInsight 클러스터를 정상적으로 만들었으므로 다음을 사용하여 클러스터 작업을 수행하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="00a67-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="00a67-160">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="00a67-160">Hadoop clusters</span></span>

* [<span data-ttu-id="00a67-161">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="00a67-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="00a67-162">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="00a67-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="00a67-163">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="00a67-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="00a67-164">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="00a67-164">HBase clusters</span></span>

* [<span data-ttu-id="00a67-165">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="00a67-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="00a67-166">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="00a67-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="00a67-167">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="00a67-167">Storm clusters</span></span>

* [<span data-ttu-id="00a67-168">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="00a67-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="00a67-169">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="00a67-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="00a67-170">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="00a67-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
