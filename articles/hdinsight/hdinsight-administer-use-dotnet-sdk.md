---
title: ".NET SDK를 사용하여 HDInsight의 Hadoop 클러스터 관리 - Azure | Microsoft Docs"
description: "HDInsight .NET SDK를 사용하여 HDInsight에서 Hadoop 클러스터에 대해 관리 작업을 수행하는 방법에 대해 알아봅니다."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: fd134765-c2a0-488a-bca6-184d814d78e9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c10471425fa1202ddb7fe35d0adf4ef33509f268
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="0776e-103">.NET SDK를 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="0776e-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="0776e-104">[HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)를 사용하여 HDInsight 클러스터를 관리하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-104">Learn how to manage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="0776e-105">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="0776e-105">**Prerequisites**</span></span>

<span data-ttu-id="0776e-106">이 문서를 시작하기 전에 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-106">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="0776e-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="0776e-107">**An Azure subscription**.</span></span> <span data-ttu-id="0776e-108">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-to-azure-hdinsight"></a><span data-ttu-id="0776e-109">Azure HDInsight에 연결</span><span class="sxs-lookup"><span data-stu-id="0776e-109">Connect to Azure HDInsight</span></span>

<span data-ttu-id="0776e-110">다음 NuGet 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-110">You need the following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="0776e-111">다음 코드 샘플은 Azure 구독에서 HDInsight 클러스터를 관리할 수 있기 전에 Azure에 연결하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-111">The following code sample shows you how to connect to Azure before you can administer HDInsight clusters under your Azure subscription.</span></span>

    using System;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;

    namespace HDInsightManagement
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // This is the GUID for the PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            static void Main(string[] args)
            {
                // Authenticate and get a token
                var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // insert code here

                System.Console.WriteLine("Press ENTER to continue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate to an Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
            {
                var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
                var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/", 
                    ClientId, 
                    new Uri("urn:ietf:wg:oauth:2.0:oob"), 
                    PromptBehavior.Always, 
                    UserIdentifier.AnyUser);
                return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
            }
            /// <summary>
            /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
            /// </summary>
            /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
            /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
            /// <param name="authToken">An authentication token for your Azure subscription</param>
            static void EnableHDInsight(TokenCloudCredentials authToken)
            {
                // Create a client for the Resource manager and set the subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register the HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="0776e-112">이 프로그램을 실행하면 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="0776e-113">프롬프트를 표시하지 않으려면 [비대화형 인증 .NET HDInsight 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-113">If you don't want to see the prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="0776e-114">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="0776e-114">Create clusters</span></span>
<span data-ttu-id="0776e-115">[.NET SDK를 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="0776e-115">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="0776e-116">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="0776e-116">List clusters</span></span>
<span data-ttu-id="0776e-117">다음 코드 조각은 클러스터 및 일부 속성을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-117">The following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="0776e-118">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="0776e-118">Delete clusters</span></span>
<span data-ttu-id="0776e-119">다음 코드 조각을 사용하여 동기적 또는 비동기적으로 클러스터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-119">Use the following code snippet to delete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="0776e-120">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="0776e-120">Scale clusters</span></span>
<span data-ttu-id="0776e-121">클러스터 크기 조정 기능을 사용하여 클러스터를 다시 생성하지 않고 Azure HDInsight에서 실행되는 클러스터에서 사용되는 작업자 노드 수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-121">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="0776e-122">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="0776e-123">클러스터 버전을 알 수 없는 경우 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-123">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="0776e-124">[클러스터 나열 및 표시](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="0776e-125">HDInsight에서 지원되는 클러스터의 각 형식에 대한 데이터 노드 수를 변경하는 영향은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-125">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="0776e-126">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="0776e-126">Hadoop</span></span>
  
    <span data-ttu-id="0776e-127">모든 보류 중인 또는 실행 중인 작업에 영향을 주지 않고 실행되는 Hadoop 클러스터의 작업자 노드 수를 원활하게 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-127">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="0776e-128">작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-128">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="0776e-129">크기 조정 작업의 오류는 정상적으로 처리되므로 클러스터는 항상 기능 상태로 남아 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-129">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="0776e-130">데이터 노드 수를 줄여 Hadoop 클러스터를 축소하면 클러스터의 서비스 중 일부가 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-130">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="0776e-131">그러면 실행 중인 작업과 보류 중인 작업이 크기 조정 작업을 완료하지 못하고 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-131">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="0776e-132">그러나 작업이 완료되면 작업을 다시 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-132">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="0776e-133">HBase</span><span class="sxs-lookup"><span data-stu-id="0776e-133">HBase</span></span>
  
    <span data-ttu-id="0776e-134">HBase 클러스터가 실행 중인 동안 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-134">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="0776e-135">지역 서버는 크기 조정 작업을 완료하는 몇 분 안에 자동으로 균형을 맞춥니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-135">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="0776e-136">그러나 클러스터의 헤드 노드에 로그인한 다음 명령 프롬프트 창에서 다음 명령을 실행하여 자동으로 지역 서버의 균형을 맞출 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-136">However, you can also manually balance the regional servers by logging into the headnode of cluster and running the following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="0776e-137">Storm</span><span class="sxs-lookup"><span data-stu-id="0776e-137">Storm</span></span>
  
    <span data-ttu-id="0776e-138">실행 중인 동안 Storm 클러스터에 데이터 노드를 원활하게 추가하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-138">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="0776e-139">하지만 크기 조정 작업이 성공적으로 완료되면 다시 토폴로지 균형을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-139">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>
  
    <span data-ttu-id="0776e-140">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="0776e-141">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="0776e-141">Storm web UI</span></span>
  * <span data-ttu-id="0776e-142">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="0776e-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="0776e-143">자세한 내용은 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) (영문)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-143">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="0776e-144">Storm 웹 UI는 HDInsight 클러스터에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-144">The Storm web UI is available on the HDInsight cluster:</span></span>
    
    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="0776e-146">다음은 CLI 명령을 사용하여 Storm 토폴로지 균형을 다시 조정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-146">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>
    
        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="0776e-147">다음 코드 조각은 동기적 또는 비동기적으로 클러스터의 크기를 조정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-147">The following code snippet shows how to resize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="0776e-148">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="0776e-148">Grant/revoke access</span></span>
<span data-ttu-id="0776e-149">HDInsight 클러스터에는 다음과 같은 HTTP 웹 서비스가 있습니다(이러한 모든 서비스에 RESTful 끝점이 있음).</span><span class="sxs-lookup"><span data-stu-id="0776e-149">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="0776e-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="0776e-150">ODBC</span></span>
* <span data-ttu-id="0776e-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="0776e-151">JDBC</span></span>
* <span data-ttu-id="0776e-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="0776e-152">Ambari</span></span>
* <span data-ttu-id="0776e-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="0776e-153">Oozie</span></span>
* <span data-ttu-id="0776e-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="0776e-154">Templeton</span></span>

<span data-ttu-id="0776e-155">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-155">By default, these services are granted for access.</span></span> <span data-ttu-id="0776e-156">액세스 권한을 해지/부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-156">You can revoke/grant the access.</span></span> <span data-ttu-id="0776e-157">해지하려면:</span><span class="sxs-lookup"><span data-stu-id="0776e-157">To revoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="0776e-158">권한하려면:</span><span class="sxs-lookup"><span data-stu-id="0776e-158">To grant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="0776e-159">액세스 권한을 부여/해지하여 클러스터 사용자 이름 및 암호를 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-159">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="0776e-160">이 작업은 포털을 통해서도 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-160">This can also be done via the Portal.</span></span> <span data-ttu-id="0776e-161">[Azure Portal을 사용하여 HDInsight 관리][hdinsight-admin-portal]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-161">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="0776e-162">HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="0776e-162">Update HTTP user credentials</span></span>
<span data-ttu-id="0776e-163">이는 [HTTP 권한 부여/해지 액세스](#grant/revoke-access)와 절차가 동일합니다. 클러스터에 HTTP 액세스 권한이 부여되어 있는 경우 이를 먼저 해지해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-163">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="0776e-164">그런 다음 새 HTTP 사용자 자격 증명을 사용하여 액세스 권한을 부여합니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-164">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="0776e-165">기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="0776e-165">Find the default storage account</span></span>
<span data-ttu-id="0776e-166">다음 코드 조각에서는 클러스터에 대한 기본 저장소 계정 이름 및 기본 저장소 계정 키를 가져오는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0776e-166">The following code snippet demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="0776e-167">작업 제출</span><span class="sxs-lookup"><span data-stu-id="0776e-167">Submit jobs</span></span>
<span data-ttu-id="0776e-168">**MapReduce 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="0776e-168">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="0776e-169">[HDInsight에서 Hadoop MapReduce 샘플 실행](hdinsight-hadoop-run-samples-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="0776e-170">**Hive 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="0776e-170">**To submit Hive jobs**</span></span> 

<span data-ttu-id="0776e-171">[.NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="0776e-172">**Pig 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="0776e-172">**To submit Pig jobs**</span></span>

<span data-ttu-id="0776e-173">[.NET SDK를 사용하여 Pig 작업 실행](hdinsight-hadoop-use-pig-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="0776e-174">**Sqoop 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="0776e-174">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="0776e-175">[HDInsight와 함께 Sqoop 사용](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="0776e-176">**Oozie 작업을 제출하려면**</span><span class="sxs-lookup"><span data-stu-id="0776e-176">**To submit Oozie jobs**</span></span>

<span data-ttu-id="0776e-177">[Hadoop과 함께 Oozie를 사용하여 HDInsight에서 워크플로 정의 및 실행](hdinsight-use-oozie-linux-mac.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-177">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="0776e-178">Azure Blob 저장소에 데이터 업로드</span><span class="sxs-lookup"><span data-stu-id="0776e-178">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="0776e-179">[HDInsight에 데이터 업로드][hdinsight-upload-data]를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0776e-179">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="0776e-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0776e-180">See Also</span></span>
* [<span data-ttu-id="0776e-181">HDInsight .NET SDK 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="0776e-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="0776e-182">[Azure Portal을 사용하여 HDInsight 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="0776e-182">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="0776e-183">[명령줄 인터페이스를 사용하여 HDInsight 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="0776e-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="0776e-184">[HDInsight 클러스터 만들기][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="0776e-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="0776e-185">[HDInsight에 데이터 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="0776e-185">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="0776e-186">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="0776e-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-portal-linux.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md


