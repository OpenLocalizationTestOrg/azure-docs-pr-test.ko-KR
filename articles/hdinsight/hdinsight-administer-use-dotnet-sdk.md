---
title: ".NET sdk-Azure HDInsight 클러스터를 aaaManage Hadoop | Microsoft Docs"
description: "방식과 tooperform 관리 작업 hello에 대 한 HDInsight.NET SDK를 사용 하 여 HDInsight의 Hadoop 클러스터에 알아봅니다."
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
ms.openlocfilehash: d8bbf966b7eba3e943dfb2f764d15d8e52b9be71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-net-sdk"></a><span data-ttu-id="e4b35-103">.NET SDK를 사용하여 HDInsight의 Hadoop 클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="e4b35-103">Manage Hadoop clusters in HDInsight by using .NET SDK</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="e4b35-104">Toomanage HDInsight 클러스터를 사용 하 여 하는 방법에 대해 알아봅니다 [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-104">Learn how toomanage HDInsight clusters using [HDInsight.NET SDK](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>

<span data-ttu-id="e4b35-105">**필수 구성 요소**</span><span class="sxs-lookup"><span data-stu-id="e4b35-105">**Prerequisites**</span></span>

<span data-ttu-id="e4b35-106">이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-106">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e4b35-107">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="e4b35-107">**An Azure subscription**.</span></span> <span data-ttu-id="e4b35-108">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-108">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="connect-tooazure-hdinsight"></a><span data-ttu-id="e4b35-109">TooAzure HDInsight 연결</span><span class="sxs-lookup"><span data-stu-id="e4b35-109">Connect tooAzure HDInsight</span></span>

<span data-ttu-id="e4b35-110">Nuget 패키지를 다음 hello가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-110">You need hello following Nuget packages:</span></span>

    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight

<span data-ttu-id="e4b35-111">hello 다음 코드 샘플 보여 줍니다 tooconnect tooAzure HDInsight 관리 하려면 Azure 구독에서 클러스터 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="e4b35-111">hello following code sample shows you how tooconnect tooAzure before you can administer HDInsight clusters under your Azure subscription.</span></span>

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
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
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

                System.Console.WriteLine("Press ENTER toocontinue");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
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
                // Create a client for hello Resource manager and set hello subscription ID
                var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
                resourceManagementClient.SubscriptionId = SubscriptionId;
                // Register hello HDInsight provider
                var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
            }
        }
    }

<span data-ttu-id="e4b35-112">이 프로그램을 실행하면 프롬프트가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-112">You shall see a prompt when you run this program.</span></span>  <span data-ttu-id="e4b35-113">Toosee hello 프롬프트를 사용 하지 않으려는 경우 참조 [비 대화형 인증 HDInsight.NET 응용 프로그램을 만들](hdinsight-create-non-interactive-authentication-dotnet-applications.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-113">If you don't want toosee hello prompt, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

## <a name="create-clusters"></a><span data-ttu-id="e4b35-114">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e4b35-114">Create clusters</span></span>
<span data-ttu-id="e4b35-115">참조 [만들 Linux 기반 클러스터에서 HDInsight를 사용 하 여 hello.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="e4b35-115">See [Create Linux-based clusters in HDInsight using hello .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="e4b35-116">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="e4b35-116">List clusters</span></span>
<span data-ttu-id="e4b35-117">hello 다음 코드 조각 클러스터 및 속성을 나열 일부:</span><span class="sxs-lookup"><span data-stu-id="e4b35-117">hello following code snippet lists clusters and some properties:</span></span>

    var results = _hdiManagementClient.Clusters.List();
    foreach (var name in results.Clusters) {
        Console.WriteLine("Cluster Name: " + name.Name);
        Console.WriteLine("\t Cluster type: " + name.Properties.ClusterDefinition.ClusterType);
        Console.WriteLine("\t Cluster location: " + name.Location);
        Console.WriteLine("\t Cluster version: " + name.Properties.ClusterVersion);
    }

## <a name="delete-clusters"></a><span data-ttu-id="e4b35-118">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="e4b35-118">Delete clusters</span></span>
<span data-ttu-id="e4b35-119">동기적 또는 비동기적으로 코드 조각 toodelete 클러스터 다음 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-119">Use hello following code snippet toodelete a cluster synchronously or asynchronously:</span></span> 

    _hdiManagementClient.Clusters.Delete("<Resource Group Name>", "<Cluster Name>");
    _hdiManagementClient.Clusters.DeleteAsync("<Resource Group Name>", "<Cluster Name>");

## <a name="scale-clusters"></a><span data-ttu-id="e4b35-120">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e4b35-120">Scale clusters</span></span>
<span data-ttu-id="e4b35-121">hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-121">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e4b35-122">HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-122">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="e4b35-123">클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-123">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="e4b35-124">[클러스터 나열 및 표시](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-124">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
> 
> 

<span data-ttu-id="e4b35-125">hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:</span><span class="sxs-lookup"><span data-stu-id="e4b35-125">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="e4b35-126">Hadoop은</span><span class="sxs-lookup"><span data-stu-id="e4b35-126">Hadoop</span></span>
  
    <span data-ttu-id="e4b35-127">원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-127">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="e4b35-128">Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-128">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="e4b35-129">크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-129">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>
  
    <span data-ttu-id="e4b35-130">Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-130">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="e4b35-131">이렇게 하면 실행 중인 모든와 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중.</span><span class="sxs-lookup"><span data-stu-id="e4b35-131">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="e4b35-132">그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-132">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="e4b35-133">HBase</span><span class="sxs-lookup"><span data-stu-id="e4b35-133">HBase</span></span>
  
    <span data-ttu-id="e4b35-134">원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-134">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="e4b35-135">지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-135">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="e4b35-136">그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 hello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-136">However, you can also manually balance hello regional servers by logging into hello headnode of cluster and running hello following commands from a command prompt window:</span></span>
  
        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="e4b35-137">Storm</span><span class="sxs-lookup"><span data-stu-id="e4b35-137">Storm</span></span>
  
    <span data-ttu-id="e4b35-138">원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-138">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="e4b35-139">하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-139">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>
  
    <span data-ttu-id="e4b35-140">다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-140">Rebalancing can be accomplished in two ways:</span></span>
  
  * <span data-ttu-id="e4b35-141">Storm 웹 UI</span><span class="sxs-lookup"><span data-stu-id="e4b35-141">Storm web UI</span></span>
  * <span data-ttu-id="e4b35-142">명령줄 인터페이스(CLI) 도구</span><span class="sxs-lookup"><span data-stu-id="e4b35-142">Command-line interface (CLI) tool</span></span>
    
    <span data-ttu-id="e4b35-143">Toohello를 참조 하십시오 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 자세한 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-143">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>
    
    <span data-ttu-id="e4b35-144">hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-144">hello Storm web UI is available on hello HDInsight cluster:</span></span>
    
    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight-portal-scale-cluster-storm-rebalance.png)
    
    <span data-ttu-id="e4b35-146">다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:</span><span class="sxs-lookup"><span data-stu-id="e4b35-146">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>
    
        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="e4b35-147">다음 코드 조각에 나와 있는 어떻게 hello tooresize 클러스터 대기가 동기적인 또는 비동기적인지:</span><span class="sxs-lookup"><span data-stu-id="e4b35-147">hello following code snippet shows how tooresize a cluster synchronously or asynchronously:</span></span>

    _hdiManagementClient.Clusters.Resize("<Resource Group Name>", "<Cluster Name>", <New Size>);   
    _hdiManagementClient.Clusters.ResizeAsync("<Resource Group Name>", "<Cluster Name>", <New Size>);   


## <a name="grantrevoke-access"></a><span data-ttu-id="e4b35-148">액세스 권한 부여/해지</span><span class="sxs-lookup"><span data-stu-id="e4b35-148">Grant/revoke access</span></span>
<span data-ttu-id="e4b35-149">HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:</span><span class="sxs-lookup"><span data-stu-id="e4b35-149">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="e4b35-150">ODBC</span><span class="sxs-lookup"><span data-stu-id="e4b35-150">ODBC</span></span>
* <span data-ttu-id="e4b35-151">JDBC</span><span class="sxs-lookup"><span data-stu-id="e4b35-151">JDBC</span></span>
* <span data-ttu-id="e4b35-152">Ambari</span><span class="sxs-lookup"><span data-stu-id="e4b35-152">Ambari</span></span>
* <span data-ttu-id="e4b35-153">Oozie</span><span class="sxs-lookup"><span data-stu-id="e4b35-153">Oozie</span></span>
* <span data-ttu-id="e4b35-154">Templeton</span><span class="sxs-lookup"><span data-stu-id="e4b35-154">Templeton</span></span>

<span data-ttu-id="e4b35-155">이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-155">By default, these services are granted for access.</span></span> <span data-ttu-id="e4b35-156">있습니다 수 revoke/hello 액세스를 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-156">You can revoke/grant hello access.</span></span> <span data-ttu-id="e4b35-157">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="e4b35-157">toorevoke:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = false,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);

<span data-ttu-id="e4b35-158">toogrant:</span><span class="sxs-lookup"><span data-stu-id="e4b35-158">toogrant:</span></span>

    var httpParams = new HttpSettingsParameters
    {
        HttpUserEnabled = enable,
        HttpUsername = "admin",
        HttpPassword = "*******",
    };
    _hdiManagementClient.Clusters.ConfigureHttpSettings("<Resource Group Name>, <Cluster Name>, httpParams);


> [!NOTE]
> <span data-ttu-id="e4b35-159">Hello 액세스 권한을 부여/취소를 하 여 hello 클러스터 사용자 이름 및 암호를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-159">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
> 
> 

<span data-ttu-id="e4b35-160">이 hello 포털을 통해 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-160">This can also be done via hello Portal.</span></span> <span data-ttu-id="e4b35-161">참조 [관리할 HDInsight를 사용 하 여 Azure 포털 hello][hdinsight-admin-portal]합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-161">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="e4b35-162">HTTP 사용자 자격 증명 업데이트</span><span class="sxs-lookup"><span data-stu-id="e4b35-162">Update HTTP user credentials</span></span>
<span data-ttu-id="e4b35-163">동일한 hello와 프로시저 [Grant/revoke HTTP 액세스](#grant/revoke-access)합니다. Hello 클러스터 부여 된 경우에 hello HTTP 액세스를 먼저 취소 해야 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-163">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="e4b35-164">한 다음 새 HTTP 사용자 자격 증명을 사용 하 여 hello 액세스 권한을 부여 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-164">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="e4b35-165">Hello 기본 저장소 계정 찾기</span><span class="sxs-lookup"><span data-stu-id="e4b35-165">Find hello default storage account</span></span>
<span data-ttu-id="e4b35-166">다음 코드 조각 hello는 방법을 보여 주는 tooget 기본 저장소 계정 이름을 hello hello 클러스터에 대 한 기본 저장소 계정 키입니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-166">hello following code snippet demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    var results = _hdiManagementClient.Clusters.GetClusterConfigurations(<Resource Group Name>, <Cluster Name>, "core-site");
    foreach (var key in results.Configuration.Keys)
    {
        Console.WriteLine(String.Format("{0} => {1}", key, results.Configuration[key]));
    }


## <a name="submit-jobs"></a><span data-ttu-id="e4b35-167">작업 제출</span><span class="sxs-lookup"><span data-stu-id="e4b35-167">Submit jobs</span></span>
<span data-ttu-id="e4b35-168">**toosubmit MapReduce 작업**</span><span class="sxs-lookup"><span data-stu-id="e4b35-168">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="e4b35-169">[HDInsight에서 Hadoop MapReduce 샘플 실행](hdinsight-hadoop-run-samples-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-169">See [Run Hadoop MapReduce samples in HDInsight](hdinsight-hadoop-run-samples-linux.md).</span></span>

<span data-ttu-id="e4b35-170">**toosubmit 하이브 작업**</span><span class="sxs-lookup"><span data-stu-id="e4b35-170">**toosubmit Hive jobs**</span></span> 

<span data-ttu-id="e4b35-171">[.NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-171">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>

<span data-ttu-id="e4b35-172">**toosubmit Pig 작업**</span><span class="sxs-lookup"><span data-stu-id="e4b35-172">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="e4b35-173">[.NET SDK를 사용하여 Pig 작업 실행](hdinsight-hadoop-use-pig-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-173">See [Run Pig jobs using .NET SDK](hdinsight-hadoop-use-pig-dotnet-sdk.md).</span></span>

<span data-ttu-id="e4b35-174">**toosubmit Sqoop 작업**</span><span class="sxs-lookup"><span data-stu-id="e4b35-174">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="e4b35-175">[HDInsight와 함께 Sqoop 사용](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4b35-175">See [Use Sqoop with HDInsight](hdinsight-hadoop-use-sqoop-dotnet-sdk.md).</span></span>

<span data-ttu-id="e4b35-176">**toosubmit Oozie 작업**</span><span class="sxs-lookup"><span data-stu-id="e4b35-176">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="e4b35-177">참조 [Hadoop toodefine 및 HDInsight에서 워크플로 실행 사용 Oozie](hdinsight-use-oozie-linux-mac.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-177">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="e4b35-178">데이터 tooAzure Blob 저장소에 업로드</span><span class="sxs-lookup"><span data-stu-id="e4b35-178">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="e4b35-179">참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.</span><span class="sxs-lookup"><span data-stu-id="e4b35-179">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="e4b35-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e4b35-180">See Also</span></span>
* [<span data-ttu-id="e4b35-181">HDInsight .NET SDK 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="e4b35-181">HDInsight .NET SDK reference documentation</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* <span data-ttu-id="e4b35-182">[HDInsight hello Azure 포털을 사용 하 여 관리][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="e4b35-182">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="e4b35-183">[명령줄 인터페이스를 사용하여 HDInsight 관리][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="e4b35-183">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="e4b35-184">[HDInsight 클러스터 만들기][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="e4b35-184">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="e4b35-185">[데이터 tooHDInsight 업로드][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e4b35-185">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e4b35-186">[Azure HDInsight 시작][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e4b35-186">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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


