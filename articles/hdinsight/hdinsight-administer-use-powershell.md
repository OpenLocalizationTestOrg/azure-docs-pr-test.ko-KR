---
title: "powershell-Azure HDInsight 클러스터를 aaaManage Hadoop | Microsoft Docs"
description: "방식과 tooperform 관리 작업 hello에 대 한 Azure PowerShell을 사용 하 여 HDInsight의 Hadoop 클러스터에 알아봅니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="45685-103">Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="45685-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="45685-104">Azure PowerShell은 toocontrol를 사용 하 고 Azure에서 작업의 hello 배포 및 관리를 자동화할 수 있는 강력한 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="45685-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="45685-105">이 문서에서는 Windows PowerShell의 hello 통해 로컬 Azure PowerShell 콘솔을 사용 하 여 Azure HDInsight의 Hadoop 클러스터 toomanage 사용 하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="45685-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="45685-106">Hello 목록이 hello HDInsight PowerShell cmdlet 참조 하십시오. [HDInsight cmdlet 참조][hdinsight-powershell-reference]합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="45685-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="45685-107">**Prerequisites**</span></span>

<span data-ttu-id="45685-108">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="45685-109">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="45685-109">**An Azure subscription**.</span></span> <span data-ttu-id="45685-110">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="45685-111">Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="45685-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="45685-112">Azure PowerShell 버전 0.9x를 설치한 경우 최신 버전을 설치하기 전에 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="45685-113">PowerShell을 설치 하는 hello의 toocheck hello 버전:</span><span class="sxs-lookup"><span data-stu-id="45685-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="45685-114">toouninstall hello 이전 버전을 hello 제어판의 프로그램 및 기능을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="45685-115">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="45685-115">Create clusters</span></span>
<span data-ttu-id="45685-116">[Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="45685-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="45685-117">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="45685-117">List clusters</span></span>
<span data-ttu-id="45685-118">Hello 현재 구독에 다음 명령을 toolist hello 모든 클러스터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="45685-119">클러스터 표시</span><span class="sxs-lookup"><span data-stu-id="45685-119">Show cluster</span></span>
<span data-ttu-id="45685-120">다음 명령은 tooshow 세부 정보 hello 현재 구독에는 특정 클러스터의 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="45685-121">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="45685-121">Delete clusters</span></span>
<span data-ttu-id="45685-122">다음 명령은 toodelete 클러스터 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="45685-123">또한 hello 클러스터를 포함 하는 hello 리소스 그룹을 제거 하 여 클러스터를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="45685-124">하십시오 note, hello 그룹의에서 모든 리소스 hello hello 기본 저장소 계정을 포함 하 여 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="45685-125">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="45685-125">Scale clusters</span></span>
<span data-ttu-id="45685-126">hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="45685-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="45685-127">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="45685-128">클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="45685-129">[클러스터 나열 및 표시](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="45685-130">hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="45685-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="45685-131">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="45685-131">Hadoop</span></span>

    <span data-ttu-id="45685-132">원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="45685-133">Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="45685-134">크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="45685-135">Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="45685-136">이렇게 하면 실행 중인 모든와 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중.</span><span class="sxs-lookup"><span data-stu-id="45685-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="45685-137">그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="45685-138">HBase</span><span class="sxs-lookup"><span data-stu-id="45685-138">HBase</span></span>

    <span data-ttu-id="45685-139">원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="45685-140">지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="45685-141">그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 toohello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="45685-142">Storm</span><span class="sxs-lookup"><span data-stu-id="45685-142">Storm</span></span>

    <span data-ttu-id="45685-143">원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="45685-144">하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="45685-145">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="45685-146">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="45685-146">Storm web UI</span></span>
  * <span data-ttu-id="45685-147">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="45685-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="45685-148">Toohello를 참조 하십시오 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="45685-149">hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="45685-151">다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="45685-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="45685-152">toochange hello hello 클라이언트 컴퓨터에서 다음 명령을 실행 하는 Azure PowerShell을 사용 하 여 Hadoop 클러스터 크기:</span><span class="sxs-lookup"><span data-stu-id="45685-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="45685-153">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="45685-153">Grant/revoke access</span></span>
<span data-ttu-id="45685-154">HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="45685-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="45685-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="45685-155">ODBC</span></span>
* <span data-ttu-id="45685-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="45685-156">JDBC</span></span>
* <span data-ttu-id="45685-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="45685-157">Ambari</span></span>
* <span data-ttu-id="45685-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="45685-158">Oozie</span></span>
* <span data-ttu-id="45685-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="45685-159">Templeton</span></span>

<span data-ttu-id="45685-160">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="45685-160">By default, these services are granted for access.</span></span> <span data-ttu-id="45685-161">있습니다 수 revoke/hello 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="45685-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="45685-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="45685-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="45685-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="45685-164">Hello 액세스 권한을 부여/취소를 하 여 hello 클러스터 사용자 이름 및 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="45685-165">이 hello 포털을 통해 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="45685-166">참조 [관리할 HDInsight를 사용 하 여 Azure 포털 hello][hdinsight-admin-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="45685-167">HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="45685-167">Update HTTP user credentials</span></span>
<span data-ttu-id="45685-168">동일한 hello와 프로시저 [Grant/revoke HTTP 액세스](#grant/revoke-access)합니다. Hello 클러스터 부여 된 경우에 hello HTTP 액세스를 먼저 취소 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="45685-169">한 다음 새 HTTP 사용자 자격 증명을 사용 하 여 hello 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="45685-170">Hello 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="45685-170">Find hello default storage account</span></span>
<span data-ttu-id="45685-171">Powershell 스크립트 뒤 hello tooget hello 기본 저장소 계정 이름 및 클러스터에 대 한 기본 저장소 계정 키를 hello 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="45685-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="45685-172">Hello 리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="45685-172">Find hello resource group</span></span>
<span data-ttu-id="45685-173">Hello 리소스 관리자 모드에서는 각 HDInsight 클러스터 tooan Azure 리소스 그룹을 속해 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45685-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="45685-174">toofind hello 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="45685-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="45685-175">작업 제출</span><span class="sxs-lookup"><span data-stu-id="45685-175">Submit jobs</span></span>
<span data-ttu-id="45685-176">**toosubmit MapReduce 작업**</span><span class="sxs-lookup"><span data-stu-id="45685-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="45685-177">[Windows 기반 HDInsight에서 Hadoop MapReduce 샘플 실행](hdinsight-run-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="45685-178">**toosubmit 하이브 작업**</span><span class="sxs-lookup"><span data-stu-id="45685-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="45685-179">[PowerShell을 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="45685-180">**toosubmit Pig 작업**</span><span class="sxs-lookup"><span data-stu-id="45685-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="45685-181">[PowerShell을 사용하여 Pig 작업 실행](hdinsight-hadoop-use-pig-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="45685-182">**toosubmit Sqoop 작업**</span><span class="sxs-lookup"><span data-stu-id="45685-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="45685-183">[HDInsight와 함께 Sqoop 사용](hdinsight-use-sqoop.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="45685-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="45685-184">**toosubmit Oozie 작업**</span><span class="sxs-lookup"><span data-stu-id="45685-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="45685-185">참조 [Hadoop toodefine 및 HDInsight에서 워크플로 실행 사용 Oozie](hdinsight-use-oozie.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="45685-186">데이터 tooAzure Blob 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="45685-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="45685-187">참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.</span><span class="sxs-lookup"><span data-stu-id="45685-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="45685-188">참고 항목</span><span class="sxs-lookup"><span data-stu-id="45685-188">See Also</span></span>
* <span data-ttu-id="45685-189">[HDInsight Cmdlet 참조 설명서][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="45685-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="45685-190">[HDInsight hello Azure 포털을 사용 하 여 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="45685-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="45685-191">[명령줄 인터페이스를 사용하여 HDInsight 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="45685-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="45685-192">[HDInsight 클러스터 만들기][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="45685-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="45685-193">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="45685-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="45685-194">[프로그래밍 방식으로 Hadoop 작업 제출][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="45685-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="45685-195">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="45685-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
