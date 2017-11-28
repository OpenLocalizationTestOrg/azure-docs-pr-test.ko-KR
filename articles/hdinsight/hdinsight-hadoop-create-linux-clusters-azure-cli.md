---
title: "hello 명령줄-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "Toocreate HDInsight 클러스터를 사용 하 여 플랫폼 간 Azure CLI 1.0 hello 하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="a8662-103">Hello Azure CLI를 사용 하 여 HDInsight 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="a8662-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="a8662-104">이 문서 연습이 hello Azure CLI 1.0을 사용 하 여 3.5 HDInsight 클러스터 만들기의 hello 단계.</span><span class="sxs-lookup"><span data-stu-id="a8662-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8662-105">Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a8662-106">자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8662-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a8662-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="a8662-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="a8662-108">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="a8662-108">**An Azure subscription**.</span></span> <span data-ttu-id="a8662-109">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8662-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="a8662-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="a8662-110">**Azure CLI**.</span></span> <span data-ttu-id="a8662-111">이 문서의 단계 hello Azure CLI 버전 0.10.14와 마지막 테스트 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a8662-112">이 문서의 단계 hello Azure CLI 2.0과 함께 작동 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="a8662-113">Azure CLI 2.0은 HDInsight 클러스터 만들기를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="a8662-114">Azure 구독 tooyour에 로그인</span><span class="sxs-lookup"><span data-stu-id="a8662-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="a8662-115">설명 하는 hello 단계에 따라 [hello Azure CLI (명령줄 인터페이스 Azure)에서 tooan Azure 구독 연결](../xplat-cli-connect.md) hello를 사용 하 여 tooyour 구독을 연결 하 고 **로그인** 메서드.</span><span class="sxs-lookup"><span data-stu-id="a8662-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="a8662-116">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a8662-116">Create a cluster</span></span>

<span data-ttu-id="a8662-117">단계를 수행 하는 hello PowerShell 또는 Bash 등의 명령줄에서 수행 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="a8662-118">사용 하 여 hello 다음 명령 tooauthenticate tooyour Azure 구독을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="a8662-119">사용자 이름 및 암호 입력 정보 요청된 tooprovide 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="a8662-120">여러 Azure 구독이 있으면 사용 하 여 `azure account set <subscriptionname>` Azure CLI hello tooset hello 구독 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="a8662-121">다음 명령을 hello를 사용 하 여 tooAzure 리소스 관리자 모드를 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="a8662-122">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-122">Create a resource group.</span></span> <span data-ttu-id="a8662-123">이 리소스 그룹 hello HDInsight 클러스터를 포함 하 고 연결 된 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="a8662-124">대체 `groupname` hello 그룹에 대 한 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="a8662-125">대체 `location` toocreate hello 그룹에서 원하는 hello 지리적 지역에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="a8662-126">목록이 유효한 위치에 대 한 hello를 사용 하 여 `azure location list` 명령을 실행 하 고 다음 hello에서 hello 위치 중 하나를 사용 하 여 `Name` 열입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="a8662-127">저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-127">Create a storage account.</span></span> <span data-ttu-id="a8662-128">이 저장소 계정은 hello HDInsight 클러스터에 대 한 hello 기본 저장소로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="a8662-129">대체 `groupname` hello 이전 단계에서 만든 hello 그룹의 hello 이름으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="a8662-130">대체 `location` hello 이전 단계에서 동일한 위치에 사용 되는 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="a8662-131">대체 `storagename` hello 저장소 계정에 대 한 고유한 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="a8662-132">이 명령을 사용 하는 hello 매개 변수에 대 한 자세한 내용은 사용 하 여 `azure storage account create -h` 이 명령에 대 한 tooview 도움말입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="a8662-133">검색 hello 키 tooaccess hello 저장소 계정을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="a8662-134">대체 `groupname` hello 리소스 그룹 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="a8662-135">대체 `storagename` hello hello 저장소 계정의 이름으로 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="a8662-136">반환 되는 hello 데이터 저장 hello `key` 값 `key1`합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="a8662-137">HDInsight 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="a8662-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="a8662-138">대체 `groupname` hello 리소스 그룹 이름을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="a8662-139">대체 `Hadoop` toocreate 한다고 hello 클러스터 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="a8662-140">예를 들어 `Hadoop`, `HBase`, `Kafka`, `Spark` 또는 `Storm`입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="a8662-141">HDInsight 클러스터 hello 기술에 대 한 튜닝 또는 클러스터 해당 toohello 작업 부하는 다양 한 형식으로 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="a8662-142">Storm 및 한 개의 클러스터에서 HBase 같은 여러 형식을 결합 하는 클러스터는 지원 되는 방법은 toocreate 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="a8662-143">대체 `location` 이전 단계에서 사용 되는 동일한 위치 hello로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="a8662-144">대체 `storagename` 을 hello 저장소 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="a8662-145">대체 `storagekey` hello 이전 단계에서 얻은 hello 키입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="a8662-146">Hello에 대 한 `--defaultStorageContainer` 매개 변수를 사용 하 여 hello hello 클러스터에 대 한 사용 하 여 이름을 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="a8662-147">대체 `admin` 및 `httppassword` hello 이름 및 암호로 원하는 toouse HTTPS를 통해 hello 클러스터에 액세스할 때.</span><span class="sxs-lookup"><span data-stu-id="a8662-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="a8662-148">대체 `sshuser` 및 `sshuserpassword` hello 사용자 이름 및 암호와 함께 원하는 toouse SSH를 사용 하 여 hello 클러스터에 액세스할 때</span><span class="sxs-lookup"><span data-stu-id="a8662-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="a8662-149">이 예제에서는 2개의 작업자 노드를 사용하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="a8662-150">크기 조정 작업을 수행 하 여 클러스터를 만든 후 hello 작업자 노드 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="a8662-151">사용하려는 작업자 노드 수가 32개를 초과하는 경우 최소한 코어 8개와 14GB RAM을 가진 헤드 노드 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="a8662-152">Hello를 사용 하 여 hello 헤드 노드 크기를 설정할 수 있습니다 `--headNodeSize` 클러스터를 만드는 동안 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="a8662-153">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8662-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="a8662-154">클러스터 만들기 프로세스 toofinish hello에 대 일 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="a8662-155">일반적으로 약 15분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="a8662-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="a8662-156">문제 해결</span><span class="sxs-lookup"><span data-stu-id="a8662-156">Troubleshoot</span></span>

<span data-ttu-id="a8662-157">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a8662-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8662-158">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a8662-158">Next steps</span></span>

<span data-ttu-id="a8662-159">Hello Azure CLI를 사용 하 여 HDInsight 클러스터를 성공적으로 만든 했으므로 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork:</span><span class="sxs-lookup"><span data-stu-id="a8662-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="a8662-160">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="a8662-160">Hadoop clusters</span></span>

* [<span data-ttu-id="a8662-161">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="a8662-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a8662-162">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="a8662-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="a8662-163">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="a8662-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="a8662-164">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="a8662-164">HBase clusters</span></span>

* [<span data-ttu-id="a8662-165">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="a8662-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="a8662-166">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="a8662-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="a8662-167">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="a8662-167">Storm clusters</span></span>

* [<span data-ttu-id="a8662-168">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="a8662-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="a8662-169">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="a8662-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="a8662-170">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="a8662-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
