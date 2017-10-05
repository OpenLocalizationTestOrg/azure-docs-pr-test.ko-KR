---
title: "PowerShell을 사용하여 HDInsight에서 Hadoop 클러스터 관리 - Azure | Microsoft Docs"
description: "Azure PowerShell을 사용하여 HDInsight에서 Hadoop 클러스터에 대해 관리 작업을 수행하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="f7f38-103">Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="f7f38-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="f7f38-104">Azure PowerShell은 Azure에서 작업의 배포와 관리를 제어 및 자동화하기 위해 사용할 수 있는 강력한 스크립팅 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="f7f38-105">이 문서에서는 Windows PowerShell을 통해 로컬 Azure PowerShell 콘솔을 사용하여 Azure HDInsight의 Hadoop 클러스터를 관리하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="f7f38-106">HDInsight PowerShell cmdlet의 목록은 [HDInsight cmdlet 참조][hdinsight-powershell-reference]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="f7f38-107">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="f7f38-107">**Prerequisites**</span></span>

<span data-ttu-id="f7f38-108">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f7f38-109">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="f7f38-109">**An Azure subscription**.</span></span> <span data-ttu-id="f7f38-110">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="f7f38-111">Azure PowerShell 설치</span><span class="sxs-lookup"><span data-stu-id="f7f38-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="f7f38-112">Azure PowerShell 버전 0.9x를 설치한 경우 최신 버전을 설치하기 전에 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="f7f38-113">설치된 PowerShell 버전을 확인하려면</span><span class="sxs-lookup"><span data-stu-id="f7f38-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="f7f38-114">이전 버전을 제거하려면 제어판에서 프로그램 및 기능을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="f7f38-115">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="f7f38-115">Create clusters</span></span>
<span data-ttu-id="f7f38-116">[Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="f7f38-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="f7f38-117">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="f7f38-117">List clusters</span></span>
<span data-ttu-id="f7f38-118">현재 구독의 클러스터를 모두 나열하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="f7f38-119">클러스터 표시</span><span class="sxs-lookup"><span data-stu-id="f7f38-119">Show cluster</span></span>
<span data-ttu-id="f7f38-120">현재 구독의 특정 클러스터 세부 정보를 표시하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="f7f38-121">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="f7f38-121">Delete clusters</span></span>
<span data-ttu-id="f7f38-122">클러스터를 삭제하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="f7f38-123">또한 클러스터를 포함하는 리소스 그룹을 제거하여 클러스터를 삭제할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="f7f38-124">이렇게 하면 기본 저장소 계정을 포함한 그룹 내 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="f7f38-125">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="f7f38-125">Scale clusters</span></span>
<span data-ttu-id="f7f38-126">클러스터 크기 조정 기능을 사용하여 클러스터를 다시 생성하지 않고 Azure HDInsight에서 실행되는 클러스터에서 사용되는 작업자 노드 수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="f7f38-127">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="f7f38-128">클러스터 버전을 알 수 없는 경우 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="f7f38-129">[클러스터 나열 및 표시](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="f7f38-130">HDInsight에서 지원되는 클러스터의 각 형식에 대한 데이터 노드 수를 변경하는 영향은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="f7f38-131">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="f7f38-131">Hadoop</span></span>

    <span data-ttu-id="f7f38-132">모든 보류 중인 또는 실행 중인 작업에 영향을 주지 않고 실행되는 Hadoop 클러스터의 작업자 노드 수를 원활하게 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="f7f38-133">작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="f7f38-134">크기 조정 작업의 오류는 정상적으로 처리되므로 클러스터는 항상 기능 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="f7f38-135">데이터 노드 수를 줄여 Hadoop 클러스터를 축소하면 클러스터의 서비스 중 일부가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="f7f38-136">그러면 실행 중인 작업과 보류 중인 작업이 크기 조정 작업을 완료하지 못하고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="f7f38-137">그러나 작업이 완료되면 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="f7f38-138">HBase</span><span class="sxs-lookup"><span data-stu-id="f7f38-138">HBase</span></span>

    <span data-ttu-id="f7f38-139">HBase 클러스터가 실행 중인 동안 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="f7f38-140">지역 서버는 크기 조정 작업을 완료하는 몇 분 안에 자동으로 균형을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="f7f38-141">그러나 클러스터의 헤드 노드에 로그인한 다음 명령 프롬프트 창에서 다음 명령을 실행하여 자동으로 지역 서버의 균형을 맞출 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="f7f38-142">Storm</span><span class="sxs-lookup"><span data-stu-id="f7f38-142">Storm</span></span>

    <span data-ttu-id="f7f38-143">실행 중인 동안 Storm 클러스터에 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="f7f38-144">하지만 크기 조정 작업이 성공적으로 완료되면 다시 토폴로지 균형을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="f7f38-145">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="f7f38-146">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="f7f38-146">Storm web UI</span></span>
  * <span data-ttu-id="f7f38-147">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="f7f38-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="f7f38-148">자세한 내용은 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="f7f38-149">Storm 웹 UI는 HDInsight 클러스터에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="f7f38-151">다음은 CLI 명령을 사용하여 Storm 토폴로지 균형을 다시 조정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="f7f38-152">Azure PowerShell을 사용하여 Hadoop 클러스터 크기를 변경하려면 클라이언트 컴퓨터에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="f7f38-153">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="f7f38-153">Grant/revoke access</span></span>
<span data-ttu-id="f7f38-154">HDInsight 클러스터에는 다음과 같은 HTTP 웹 서비스가 있습니다(이러한 모든 서비스에 RESTful 끝점이 있음).</span><span class="sxs-lookup"><span data-stu-id="f7f38-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="f7f38-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="f7f38-155">ODBC</span></span>
* <span data-ttu-id="f7f38-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="f7f38-156">JDBC</span></span>
* <span data-ttu-id="f7f38-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="f7f38-157">Ambari</span></span>
* <span data-ttu-id="f7f38-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="f7f38-158">Oozie</span></span>
* <span data-ttu-id="f7f38-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="f7f38-159">Templeton</span></span>

<span data-ttu-id="f7f38-160">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-160">By default, these services are granted for access.</span></span> <span data-ttu-id="f7f38-161">액세스 권한을 해지/부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-161">You can revoke/grant the access.</span></span> <span data-ttu-id="f7f38-162">해지하려면:</span><span class="sxs-lookup"><span data-stu-id="f7f38-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="f7f38-163">권한하려면:</span><span class="sxs-lookup"><span data-stu-id="f7f38-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="f7f38-164">액세스 권한을 부여/해지하여 클러스터 사용자 이름 및 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="f7f38-165">이 작업은 포털을 통해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-165">This can also be done via the Portal.</span></span> <span data-ttu-id="f7f38-166">[Azure Portal을 사용하여 HDInsight 관리][hdinsight-admin-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="f7f38-167">HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="f7f38-167">Update HTTP user credentials</span></span>
<span data-ttu-id="f7f38-168">이는 [HTTP 권한 부여/해지 액세스](#grant/revoke-access)와 절차가 동일합니다. 클러스터에 HTTP 액세스 권한이 부여되어 있는 경우 이를 먼저 해지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="f7f38-169">그런 다음 새 HTTP 사용자 자격 증명을 사용하여 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="f7f38-170">기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="f7f38-170">Find the default storage account</span></span>
<span data-ttu-id="f7f38-171">다음 Powershell 스크립트에서는 클러스터에 대한 기본 저장소 계정 이름 및 기본 저장소 계정 키를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="f7f38-172">리소스 그룹 찾기</span><span class="sxs-lookup"><span data-stu-id="f7f38-172">Find the resource group</span></span>
<span data-ttu-id="f7f38-173">Resource Manager 모드에서 각 HDInsight 클러스터는 Azure 리소스 그룹에 속합니다.</span><span class="sxs-lookup"><span data-stu-id="f7f38-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="f7f38-174">리소스 그룹을 찾으려면:</span><span class="sxs-lookup"><span data-stu-id="f7f38-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="f7f38-175">작업 제출</span><span class="sxs-lookup"><span data-stu-id="f7f38-175">Submit jobs</span></span>
<span data-ttu-id="f7f38-176">**MapReduce 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f7f38-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="f7f38-177">[Windows 기반 HDInsight에서 Hadoop MapReduce 샘플 실행](hdinsight-run-samples.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="f7f38-178">**Hive 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f7f38-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="f7f38-179">[PowerShell을 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="f7f38-180">**Pig 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f7f38-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="f7f38-181">[PowerShell을 사용하여 Pig 작업 실행](hdinsight-hadoop-use-pig-powershell.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="f7f38-182">**Sqoop 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f7f38-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="f7f38-183">[HDInsight와 함께 Sqoop 사용](hdinsight-use-sqoop.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="f7f38-184">**Oozie 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="f7f38-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="f7f38-185">[Hadoop과 함께 Oozie를 사용하여 HDInsight에서 워크플로 정의 및 실행](hdinsight-use-oozie.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="f7f38-186">Azure Blob 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="f7f38-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="f7f38-187">[HDInsight에 데이터 업로드][hdinsight-upload-data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f7f38-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="f7f38-188">참고 항목</span><span class="sxs-lookup"><span data-stu-id="f7f38-188">See Also</span></span>
* <span data-ttu-id="f7f38-189">[HDInsight Cmdlet 참조 설명서][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="f7f38-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="f7f38-190">[Azure Portal을 사용하여 HDInsight 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="f7f38-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="f7f38-191">[명령줄 인터페이스를 사용하여 HDInsight 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="f7f38-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="f7f38-192">[HDInsight 클러스터 만들기][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="f7f38-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="f7f38-193">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="f7f38-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="f7f38-194">[프로그래밍 방식으로 Hadoop 작업 제출][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="f7f38-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="f7f38-195">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="f7f38-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
