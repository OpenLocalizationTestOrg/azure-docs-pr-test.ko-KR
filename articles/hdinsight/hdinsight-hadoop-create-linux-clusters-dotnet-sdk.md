---
title: ".NET-Azure HDInsight를 사용 하 여 aaaCreate Hadoop 클러스터 | Microsoft Docs"
description: "HDInsight를 사용 하 여에 대 한 linux의 toocreate Hadoop, HBase, 스톰, 또는 Spark 클러스터 HDInsight.NET SDK hello 하는 방법에 대해 알아봅니다."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9c74e3dc-837f-4c90-bbb1-489bc7124a3d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 9460b0d27143c97860b3540fcec26851d755aa28
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-net-sdk"></a><span data-ttu-id="63aea-103">Hello.NET SDK를 사용 하 여 HDInsight의 Linux 기반 클러스터를 만들려면</span><span class="sxs-lookup"><span data-stu-id="63aea-103">Create Linux-based clusters in HDInsight using hello .NET SDK</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]


<span data-ttu-id="63aea-104">사용 하 여 Azure HDInsight 클러스터에서 Hadoop 클러스터 toocreate.NET SDK hello 하는 방법에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-104">Learn how toocreate a Hadoop cluster in Azure HDInsight cluster using hello .NET SDK.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63aea-105">이 문서의 단계 hello 하나의 작업자 노드 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-105">hello steps in this document create a cluster with one worker node.</span></span> <span data-ttu-id="63aea-106">32 개 이상의 작업자 노드 클러스터 만들기 또는 hello 클러스터를 만든 후 확장 하 여 계획 이라면 tooselect 적어도 8 개 코어 및 14GB ram에 헤드 노드 크기 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-106">If you plan on more than 32 worker nodes, either at cluster creation or by scaling hello cluster after creation, you need tooselect a head node size with at least 8 cores and 14GB ram.</span></span>
>
> <span data-ttu-id="63aea-107">노드 크기 및 관련된 비용에 대한 자세한 내용은 [HDInsight 가격 책정](https://azure.microsoft.com/pricing/details/hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-107">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63aea-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="63aea-108">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="63aea-109">**Azure 구독**.</span><span class="sxs-lookup"><span data-stu-id="63aea-109">**An Azure subscription**.</span></span> <span data-ttu-id="63aea-110">[Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="63aea-111">**Azure Storage 계정**</span><span class="sxs-lookup"><span data-stu-id="63aea-111">**An Azure storage account**.</span></span> <span data-ttu-id="63aea-112">[저장소 계정 만들기](../storage/common/storage-create-storage-account.md#create-a-storage-account)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-112">See [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>
* <span data-ttu-id="63aea-113">**Visual Studio 2013, Visual Studio 2015 또는 Visual Studio 2017**</span><span class="sxs-lookup"><span data-stu-id="63aea-113">**Visual Studio 2013, Visual Studio 2015 or Visual Studio 2017**.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="63aea-114">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="63aea-114">Create clusters</span></span>

1. <span data-ttu-id="63aea-115">Visual Studio 2017을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-115">Open Visual Studio 2017.</span></span>
2. <span data-ttu-id="63aea-116">새 Visual C# 콘솔 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-116">Create a new Visual C# console application.</span></span>
3. <span data-ttu-id="63aea-117">Hello에서 **도구** 메뉴를 클릭 하 여 **NuGet 패키지 관리자**, 클릭 하 고 **패키지 관리자 콘솔**합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-117">From hello **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
4. <span data-ttu-id="63aea-118">Hello 다음 hello 콘솔 tooinstall hello 패키지에서 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-118">Run hello following command in hello console tooinstall hello packages:</span></span>

    ```powershell
    Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
    Install-Package Microsoft.Azure.Management.ResourceManager -Pre
    Install-Package Microsoft.Azure.Management.HDInsight
    ```

    <span data-ttu-id="63aea-119">이 명령은.NET 라이브러리 및 참조 toothem toohello 현재 Visual Studio 프로젝트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-119">These commands add .NET libraries and references toothem toohello current Visual Studio project.</span></span>
5. <span data-ttu-id="63aea-120">솔루션 탐색기에서 두 번 클릭 **Program.cs** tooopen, 코드를 다음 hello를 붙여 넣고 hello 변수에 대 한 값을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-120">From Solution Explorer, double-click **Program.cs** tooopen it, paste hello following code, and provide values for hello variables:</span></span>

    ```csharp
    using System;
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure;
    using Microsoft.Azure.Management.HDInsight;
    using Microsoft.Azure.Management.HDInsight.Models;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    namespace CreateHDInsightCluster
    {
        class Program
        {
            private static HDInsightManagementClient _hdiManagementClient;

            private const string SubscriptionId = "<Your Azure Subscription ID>";
            // Replace with your AAD tenant ID if necessary
            private const string TenantId = UserTokenProvider.CommonTenantId; 
            // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
            private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";

            private const string ExistingResourceGroupName = "<Enter Resource Group Name>";
            private const string ExistingStorageName = "<Enter Default Storage Account Name>.blob.core.windows.net";
            private const string ExistingStorageKey = "<Enter Default Storage Account Key>";
            private const string ExistingBlobContainer = "<Enter Default Bob Container Name>";

            private const string NewClusterName = "<Enter HDInsight Cluster Name>";
            private const int NewClusterNumNodes = 2;
            private const string NewClusterLocation = "EAST US 2";     // Must be hello same as hello default Storage account
            private const OSType NewClusterOSType = OSType.Linux;
            private const string NewClusterType = "Hadoop";
            private const string NewClusterVersion = "3.5";
            private const string NewClusterUsername = "admin";
            private const string NewClusterPassword = "<Enter HTTP User Password>";
            private const string NewClusterSshUserName = "sshuser";

            // You can use eitehr password or public key. See https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix
            private const string NewClusterSshPassword = "<Enter SSH User Password>";
            private const string NewClusterSshPublicKey = @"---- BEGIN SSH2 PUBLIC KEY ----
                Comment: ""rsa-key-20150731""
                AAAAB3NzaC1yc2EAAAABJQAAAQEA4QiCRLqT7fnmUA5OhYWZNlZo6lLaY1c+IRsp
                gmPCsJVGQLu6O1wqcxRqiKk7keYq8bP5s30v6bIljsLZYTnyReNUa5LtFw7eauGr
                yVt3Pve6ejfWELhbVpi0iq8uJNFA9VvRkz8IP1JmjC5jsdnJhzQZtgkIrdn3w0e6
                WVfu15kKyY8YAiynVbdV51EB0SZaSLdMZkZQ81xi4DDtCZD7qvdtWEFwLa+EHdkd
                pzO36Mtev5XvseLQqzXzZ6aVBdlXoppGHXkoGHAMNOtEWRXpAUtEccjpATsaZhQR
                zZdZlzHduhM10ofS4YOYBADt9JohporbQVHM5w6qUhIgyiPo7w==
                ---- END SSH2 PUBLIC KEY ----"; //replace hello public key with your own

            static void Main(string[] args)
            {
                System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

                // Authenticate and get a token
                var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
                // Flag subscription for HDInsight, if it isn't already.
                EnableHDInsight(authToken);
                // Get an HDInsight management client
                _hdiManagementClient = new HDInsightManagementClient(authToken);

                // Set parameters for hello new cluster
                var parameters = new ClusterCreateParameters
                {
                    ClusterSizeInNodes = NewClusterNumNodes,
                    UserName = NewClusterUsername,
                    ClusterType = NewClusterType,
                    OSType = NewClusterOSType,
                    Version = NewClusterVersion,

                    // Use an Azure storage account as hello default storage
                    DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

                    // Is hello cluster type RServer? If so, you can set hello EdgeNodeSize.
                    // Otherwise, hello default VM size is used.
                    //EdgeNodeSize = "Standard_D12_v2",

                    Password = NewClusterPassword,
                    Location = NewClusterLocation,

                    SshUserName = NewClusterSshUserName,
                    SshPassword = NewClusterSshPassword,
                    //SshPublicKey = NewClusterSshPublicKey
                };

                // Is hello cluster type RServer? If so, add hello RStudio configuration option.
                /*
                parameters.Configurations.Add(
                    "rserver",
                    new Dictionary<string, string>()
                    {
                        { "rstudio", "true" }
                    }
                );
                */

                // Create hello cluster
                _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

                System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            /// <summary>
            /// Authenticate tooan Azure subscription and retrieve an authentication token
            /// </summary>
            static TokenCloudCredentials GetTokenCloudCredentials(string TenantId, string ClientId, string SubscriptionId)
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
    ```

6. <span data-ttu-id="63aea-121">Hello 클래스 멤버 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-121">Replace hello class member values.</span></span>
7. <span data-ttu-id="63aea-122">키를 눌러 **F5** toorun hello 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-122">Press **F5** toorun hello application.</span></span> <span data-ttu-id="63aea-123">콘솔 창이 열리고 hello 응용 프로그램의 hello 상태를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-123">A console window should open and display hello status of hello application.</span></span> <span data-ttu-id="63aea-124">하면 Azure 계정 자격 증명된 tooenter 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-124">You are prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="63aea-125">걸릴 수 있습니다 몇 분 toocreate HDInsight 클러스터를 일반적으로 약 15입니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-125">It can take several minutes toocreate an HDInsight cluster, normally around 15.</span></span>

## <a name="use-bootstrap"></a><span data-ttu-id="63aea-126">부트스트랩 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-126">Use bootstrap</span></span>

<span data-ttu-id="63aea-127">부트스트랩을 사용 하 여 hello 클러스터 만들기 중 추가 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-127">Using bootstrap, you can configure addition settings during hello cluster creations.</span></span>  <span data-ttu-id="63aea-128">자세한 내용은 [부트스트랩을 사용하여 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-bootstrap.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-128">For more information, see [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).</span></span>

<span data-ttu-id="63aea-129">Hello 샘플에서 수정 [클러스터를 만들어](#create-clusters) tooconfigure 하이브 설정:</span><span class="sxs-lookup"><span data-stu-id="63aea-129">Modify hello sample in [Create clusters](#create-clusters) tooconfigure a Hive setting:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var extendedParameters = new ClusterCreateParametersExtended
    {
        Location = NewClusterLocation,
        Properties = new ClusterCreateProperties
        {
            ClusterDefinition = new ClusterDefinition
            {
                ClusterType = NewClusterType.ToString()
            },
            ClusterVersion = NewClusterVersion,
            OperatingSystemType = NewClusterOSType
        }
    };

    var coreConfigs = new Dictionary<string, string>
    {
        {"fs.defaultFS", string.Format("wasb://{0}@{1}", ExistingBlobContainer, ExistingStorageName)},
        {
            string.Format("fs.azure.account.key.{0}", ExistingStorageName),
            ExistingStorageKey
        }
    };

    // bootstrap
    var hiveConfigs = new Dictionary<string, string>
    {
        { "hive.metastore.client.socket.timeout", "90"}
    };

    var gatewayConfigs = new Dictionary<string, string>
    {
        {"restAuthCredential.isEnabled", "true"},
        {"restAuthCredential.username", NewClusterUsername},
        {"restAuthCredential.password", NewClusterPassword}
    };

    var configurations = new Dictionary<string, Dictionary<string, string>>
    {
        {"core-site", coreConfigs},
        {"gateway", gatewayConfigs},
        {"hive-site", hiveConfigs}
    };

    var serializedConfig = JsonConvert.SerializeObject(configurations);
    extendedParameters.Properties.ClusterDefinition.Configurations = serializedConfig;

    var sshPublicKeys = new List<SshPublicKey>();
    var sshPublicKey = new SshPublicKey
    {
        CertificateData =
            string.Format("ssh-rsa {0}", NewClusterSshPublicKey)
    };
    sshPublicKeys.Add(sshPublicKey);

    var headNode = new Role
    {
        Name = "headnode",
        TargetInstanceCount = 2,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                // When use a SSH pulbic key, make sure tooremove comments, headers and trailers, and concatenate hello key into one line 
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    var workerNode = new Role
    {
        Name = "workernode",
        TargetInstanceCount = NewClusterNumNodes,
        HardwareProfile = new HardwareProfile
        {
            VmSize = "Large"
        },
        OsProfile = new OsProfile
        {
            LinuxOperatingSystemProfile = new LinuxOperatingSystemProfile
            {
                UserName = NewClusterSshUserName,
                Password = NewClusterSshPassword //,
                //SshProfile = new SshProfile
                //{
                //    SshPublicKeys = sshPublicKeys
                //}
            }
        }
    };

    extendedParameters.Properties.ComputeProfile = new ComputeProfile();
    extendedParameters.Properties.ComputeProfile.Roles.Add(headNode);
    extendedParameters.Properties.ComputeProfile.Roles.Add(workerNode);

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, extendedParameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="use-script-action"></a><span data-ttu-id="63aea-130">스크립트 동작 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-130">Use Script Action</span></span>

<span data-ttu-id="63aea-131">스크립트 동작을 사용하여 클러스터를 만드는 중에 추가 설정을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-131">Using Script Action, you can configure additional settings during cluster creations.</span></span>  <span data-ttu-id="63aea-132">자세한 내용은 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-132">For more information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="63aea-133">Hello 샘플에서 수정 [클러스터를 만들어](#create-clusters) toocall 스크립트 동작 tooinstall r:</span><span class="sxs-lookup"><span data-stu-id="63aea-133">Modify hello sample in [Create clusters](#create-clusters) toocall a Script Action tooinstall R:</span></span>

```csharp
static void Main(string[] args)
{
    System.Console.WriteLine("Creating a cluster.  hello process takes 10 too20 minutes ...");

    // Authenticate and get a token
    var authToken = GetTokenCloudCredentials(TenantId, ClientId, SubscriptionId);
    // Flag subscription for HDInsight, if it isn't already.
    EnableHDInsight(authToken);
    // Get an HDInsight management client
    _hdiManagementClient = new HDInsightManagementClient(authToken);

    // Set parameters for hello new cluster
    var parameters = new ClusterCreateParameters
    {
        ClusterSizeInNodes = NewClusterNumNodes,
        Location = NewClusterLocation,
        ClusterType = NewClusterType,
        OSType = NewClusterOSType,
        Version = NewClusterVersion,

        DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingBlobContainer),

        UserName = NewClusterUsername,
        Password = NewClusterPassword,
        SshUserName = NewClusterSshUserName,
        SshPublicKey = NewClusterSshPublicKey
    };

    ScriptAction rScriptAction = new ScriptAction("Install R",
        new Uri("https://hdiconfigactions.blob.core.windows.net/linuxrconfigactionv01/r-installer-v01.sh"), "");

    parameters.ScriptActions.Add(ClusterNodeType.HeadNode,new System.Collections.Generic.List<ScriptAction> { rScriptAction});
    parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { rScriptAction });

    _hdiManagementClient.Clusters.Create(ExistingResourceGroupName, NewClusterName, parameters);

    System.Console.WriteLine("hello cluster has been created. Press ENTER toocontinue ...");
    System.Console.ReadLine();
}
```

## <a name="troubleshoot"></a><span data-ttu-id="63aea-134">문제 해결</span><span class="sxs-lookup"><span data-stu-id="63aea-134">Troubleshoot</span></span>

<span data-ttu-id="63aea-135">HDInsight 클러스터를 만드는 동안 문제가 발생할 경우 [액세스 제어 요구 사항](hdinsight-administer-use-portal-linux.md#create-clusters)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="63aea-135">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63aea-136">다음 단계</span><span class="sxs-lookup"><span data-stu-id="63aea-136">Next steps</span></span>
<span data-ttu-id="63aea-137">HDInsight 클러스터를 성공적으로 만든 toolearn 방법을 따르는 hello를 사용 하 여 클러스터와 toowork 합니다.</span><span class="sxs-lookup"><span data-stu-id="63aea-137">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span> 

### <a name="hadoop-clusters"></a><span data-ttu-id="63aea-138">Hadoop 클러스터</span><span class="sxs-lookup"><span data-stu-id="63aea-138">Hadoop clusters</span></span>
* [<span data-ttu-id="63aea-139">HDInsight에서 Hive 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-139">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="63aea-140">HDInsight에서 Pig 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-140">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="63aea-141">HDInsight와 함께 MapReduce 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-141">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="63aea-142">HBase 클러스터</span><span class="sxs-lookup"><span data-stu-id="63aea-142">HBase clusters</span></span>
* [<span data-ttu-id="63aea-143">HDInsight에서 HBase 시작</span><span class="sxs-lookup"><span data-stu-id="63aea-143">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="63aea-144">HDInsight에서 HBase용 Java 응용 프로그램 개발</span><span class="sxs-lookup"><span data-stu-id="63aea-144">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="63aea-145">Storm 클러스터</span><span class="sxs-lookup"><span data-stu-id="63aea-145">Storm clusters</span></span>
* [<span data-ttu-id="63aea-146">HDInsight에서 Storm용 Java 토폴로지 개발</span><span class="sxs-lookup"><span data-stu-id="63aea-146">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="63aea-147">HDInsight의 Storm에서 Python 구성 요소 사용</span><span class="sxs-lookup"><span data-stu-id="63aea-147">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="63aea-148">HDInsight에서 Storm을 사용하는 토폴로지 배포 및 모니터링</span><span class="sxs-lookup"><span data-stu-id="63aea-148">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="63aea-149">Spark 클러스터</span><span class="sxs-lookup"><span data-stu-id="63aea-149">Spark clusters</span></span>
* [<span data-ttu-id="63aea-150">Scala를 사용하여 독립 실행형 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="63aea-150">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="63aea-151">Livy를 사용하여 Spark 클러스터에서 원격으로 작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-151">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="63aea-152">BI와 Spark: BI 도구와 함께 HDInsight에서 Spark를 사용하여 대화형 데이터 분석 수행</span><span class="sxs-lookup"><span data-stu-id="63aea-152">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="63aea-153">Spark와 기계 학습: HDInsight toopredict 음식 검사 결과에 사용 하 여 Spark</span><span class="sxs-lookup"><span data-stu-id="63aea-153">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="63aea-154">Spark 스트리밍: HDInsight에서 Spark를 사용하여 실시간 스트리밍 응용 프로그램 빌드</span><span class="sxs-lookup"><span data-stu-id="63aea-154">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="run-jobs"></a><span data-ttu-id="63aea-155">작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-155">Run jobs</span></span>
* [<span data-ttu-id="63aea-156">.NET SDK를 사용하여 HDInsight에서 Hive 작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-156">Run Hive jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-hive-dotnet-sdk.md)
* [<span data-ttu-id="63aea-157">.NET SDK를 사용하여 HDInsight에서 Pig 작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-157">Run Pig jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md)
* [<span data-ttu-id="63aea-158">.NET SDK를 사용하여 HDInsight에서 Sqoop 작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-158">Run Sqoop jobs in HDInsight using .NET SDK</span></span>](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)
* [<span data-ttu-id="63aea-159">HDInsight에서 Oozie 작업 실행</span><span class="sxs-lookup"><span data-stu-id="63aea-159">Run Oozie jobs in HDInsight</span></span>](hdinsight-use-oozie.md)

