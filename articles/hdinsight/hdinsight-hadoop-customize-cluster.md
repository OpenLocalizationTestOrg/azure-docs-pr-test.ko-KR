---
title: "aaaCustomize HDInsight 클러스터를 사용 하 여 스크립트 작업을-Azure | Microsoft Docs"
description: "Toocustomize HDInsight 클러스터 스크립트 작업을 사용 하는 방법을 알아봅니다."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a>스크립트 작업을 사용하여 Windows 기반 HDInsight 클러스터 사용자 지정
**작업 스크립트** tooinvoke 사용된 될 수 있습니다 [사용자 지정 스크립트](hdinsight-hadoop-script-actions.md) 클러스터에 추가 소프트웨어를 설치 하기 위한 hello 클러스터 만들기 프로세스 중입니다.

이 문서의 hello 정보에는 특정 tooWindows 기반 HDInsight 클러스터입니다. Linux 기반 클러스터는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

> [!IMPORTANT]
> Linux는 hello 전용 운영 체제 HDInsight 버전 3.4 이상에서 사용 합니다. 자세한 내용은 [Windows에서 HDInsight 사용 중지](hdinsight-component-versioning.md#hdinsight-windows-retirement)를 참조하세요.

Azure 저장소 계정 추가 포함 하 여 같은 다양 한 다른 방법으로,도 지정할 수 있습니다 HDInsight 클러스터, 구성 파일 (코어 site.xml, hive-site.xml 등)을, Hadoop hello를 변경 하거나 (예: 하이브, Oozie) 라이브러리에 공유 추가 hello 클러스터의 공용 위치입니다. 이러한 사용자 지정 Azure HDInsight.NET SDK hello Azure PowerShell을 통해 수행할 수 있습니다 또는 Azure 포털을 환영 합니다. 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기][hdinsight-provision-cluster]를 참조하세요.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a>Hello 클러스터 만들기 프로세스에 스크립트 동작
스크립트 동작 클러스터를 만들려는의 hello 프로세스 중인 동안에 사용 됩니다. hello 다음 다이어그램에서는 hello 만드는 프로세스 동안 스크립트 작업을 실행할 때 수행 합니다.

![HDInsight 클러스터 사용자 지정 및 클러스터 만드는 동안의 단계][img-hdi-cluster-states]

Hello 스크립트가 실행 되 고 hello 클러스터 hello 입력 **ClusterCustomization** 단계입니다. 이 단계에서는 hello 스크립트 hello 시스템 관리자 계정에서 실행, 모든 hello에 동시에 지정 된 hello 클러스터의 노드 및 hello 노드에서 모든 관리자 권한을 제공 합니다.

> [!NOTE]
> 동안 hello 클러스터 노드에 대 한 관리자 권한이 있으므로 **ClusterCustomization** 단계 Hadoop 관련 서비스를 포함 한 서비스를 시작 및 중지와 같은 hello 스크립트 tooperform 작업을 사용할 수 있습니다. Hello 스크립트의 일부로 확인 해야 하므로 해당 hello Ambari 서비스 및 다른 Hadoop 관련 서비스는 실행 되 고 hello 스크립트 실행이 완료 되기 전에 합니다. 이러한 서비스는 필요한 생성 되는 동안 toosuccessfully hello 상태 및 hello 클러스터의 상태 확인 합니다. 이러한 서비스에 영향을 주는 클러스터에서 모든 구성을 변경 하면 제공 하는 hello 도우미 함수를 사용 해야 합니다. 도우미 함수에 대한 자세한 내용은 [HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.
>
>

hello 출력 및 오류 로그를 hello hello 스크립트 hello 클러스터에 대해 지정 하는 hello 기본 저장소 계정에 저장 됩니다. hello 로그 테이블에 저장 됩니다는 hello 이름의 **u < \cluster-name-fragment >< \time-stamp > setuplog**합니다. 이들은 hello 클러스터의 모든 hello 노드 (작업자 노드 및 헤드 노드)에서 실행 하는 hello 스크립트에서 로그를 집계 합니다.

각 클러스터는 지정 된 hello 순서 대로 호출 되는 여러 스크립트 작업을 사용할 수 있습니다. 스크립트는 hello 헤드 노드, hello 작업자 노드 중 하나 또는 둘 다 실행 수 있습니다.

HDInsight는 HDInsight 클러스터에서 다음과 같은 구성 요소가 여러 스크립트 tooinstall hello를 제공 합니다.

| 이름 | 스크립트 |
| --- | --- |
| **Spark 설치** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]을 참조하세요. |
| **R 설치** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. [HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]을 참조하세요. |
| **Solr 설치** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. [HDInsight 클러스터에서 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)을 참조하세요. |
| - **Giraph 설치** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)을 참조하세요. |
| **Hive 라이브러리 사전 로드** |https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1. [HDInsight 클러스터에서 Hive 라이브러리 추가](hdinsight-hadoop-add-hive-libraries.md) |

## <a name="call-scripts-using-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여 스크립트를 호출 합니다.
**Hello Azure 포털에서**

1. [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)에서 설명한 대로 클러스터를 만들기 시작합니다.
2. Hello에 대 한 선택적 구성에서 **스크립트 동작** 블레이드에서 클릭 **스크립트 동작 추가** 아래와 같이 tooprovide hello 스크립트 동작에 대 한 세부 정보:

    ![스크립트 동작 toocustomize 클러스터를 사용 하 여](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "사용 하 여 작업 스크립팅 toocustomize 클러스터")

    <table border='1'>
        <tr><th>속성</th><th>값</th></tr>
        <tr><td>이름</td>
            <td>Hello 스크립트 동작에 대 한 이름을 지정 합니다.</td></tr>
        <tr><td>스크립트 URI</td>
            <td>가 호출 된 toocustomize hello 클러스터 hello URI toohello 스크립트를 지정 합니다. s</td></tr>
        <tr><td>헤드/작업자</td>
            <td>Hello 노드를 지정 (**h e a d** 또는 **작업자**) hello 사용자 정의 스크립트 실행.</b>합니다.
        <tr><td>매개 변수</td>
            <td>Hello 스크립트에 필요한 경우 hello 매개 변수를 지정 합니다.</td></tr>
    </table>

    하나의 스크립트 동작 tooinstall 이상 ENTER tooadd 여러 구성 요소를 눌러 hello 클러스터 합니다.
3. 클릭 **선택** toosave hello 스크립트 작업 구성 및 클러스터 만들기를 계속 합니다.

## <a name="call-scripts-using-azure-powershell"></a>Azure PowerShell을 사용하여 스크립트 호출
이 다음 PowerShell 스크립트는 Windows에서 Spark tooinstall HDInsight 클러스터를 기반 하는 방법을 보여 줍니다.  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


tooinstall 기타 소프트웨어 해야 hello 스크립트에서 tooreplace hello 스크립트 파일:

메시지가 표시 되 면 hello 클러스터에 대 한 hello 자격 증명을 입력 합니다. Hello 클러스터를 만들기 전에 몇 분 정도 걸릴 수 있습니다.

## <a name="call-scripts-using-net-sdk"></a>.NET SDK를 사용하여 스크립트 호출
hello 다음 예제에서는 Windows에서 Spark tooinstall HDInsight 클러스터를 기반 하는 방법 tooinstall 기타 소프트웨어 해야 hello 코드 tooreplace hello 스크립트 파일입니다.

**toocreate Spark와 함께 하는 HDInsight 클러스터**

1. Visual Studio를 사용하여 C# 콘솔 응용 프로그램을 만듭니다.
2. Nuget 패키지 관리자 콘솔 hello hello 다음 명령을 실행 합니다.

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. 문을 사용 하 여 hello Program.cs 파일에 다음 사용 하 여 hello:

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. Hello 다음을 사용 하 여 hello 클래스에 hello 코드를 배치 합니다.

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
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
5. 키를 눌러 **F5** toorun hello 응용 프로그램입니다.

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a>HDInsight 클러스터에서 사용하는 오픈 소스 소프트웨어 지원
Microsoft Azure HDInsight 서비스 hello Hadoop 주위 형성 하는 오픈 소스 기술 프로그램 에코 시스템을 사용 하 여 hello 클라우드에서 toobuild 빅 데이터 응용 프로그램 수 있도록 하는 유연한 플랫폼입니다. Microsoft Azure hello에 설명 된 대로 오픈 소스 기술에 대 한 일반 수준의 지원 제공 **지원 범위** hello 섹션 <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure 지원 FAQ 웹 사이트</a>합니다. hello HDInsight 서비스 아래 설명 된 대로 추가 수준의 hello 구성 요소 중 일부에 대 한 지원 제공 합니다.

Hello HDInsight 서비스에서에서 사용할 수 있는 오픈 소스 구성 요소는 다음과 같은 두 종류가 있습니다.

* **기본 제공 구성 요소** -이 구성 요소는 HDInsight 클러스터에 미리 설치 되어 하며 hello 클러스터의 핵심 기능을 제공 합니다. 예를 들어 YARN ResourceManager, hello 하이브 쿼리 언어 (HiveQL) 및 hello Mahout 라이브러리 toothis 범주에 속합니다. 클러스터 구성 요소 전체 목록은 영어로 [HDInsight에서 제공 하는 hello Hadoop 클러스터 버전의 새로운 기능?](hdinsight-component-versioning.md) </a>.
* **사용자 지정 구성 요소** -, hello 클러스터의 사용자로 설치 또는 hello 커뮤니티에서 사용할 수 있거나 사용자가 만든 모든 구성 요소를 작업에 사용 합니다.

기본 제공 구성 요소가 완전 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.

> [!WARNING]
> Hello HDInsight 클러스터와 함께 제공 되는 구성 요소 완벽 하 게 지원를 Microsoft 지원 tooisolate는 데 도움이 되며 관련된 toothese 구성 요소 문제를 해결 합니다.
>
> 사용자 지정 구성 요소 상업적으로 적절 한 지원 toohelp 수신 하면 toofurther hello 문제를 해결 합니다. 이 hello 문제를 해결 하거나 hello에 대 한 사용 가능한 채널 tooengage 열면 해당 기술에 대 한 심층 전문 지식이 있는 소스 기술을 요청 될 수 있습니다. 예를 들어 [HDInsight에 대한 MSDN 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com)과 같은 여러 커뮤니티 사이트를 사용할 수 있습니다. 또한 Apache 프로젝트에는 [http://apache.org](http://apache.org)에 프로젝트 사이트가 있습니다(예: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/)).
>
>

HDInsight 서비스 hello toouse 사용자 지정 구성 요소를 여러 가지 방법으로 제공합니다. 어떻게 구성 요소가 사용 되거나 hello 클러스터에 설치에 관계 없이 hello 동일한 지원 수준으로 적용 됩니다. 다음은 HDInsight 클러스터에서 사용자 지정 구성 요소를 사용할 수 있도록 하는 hello 가장 일반적인 방법의 목록이입니다.

1. 작업 제출-Hadoop 또는 기타 유형의 작업을 실행 하거나 사용자 지정 구성 요소를 사용 하 여 제출 된 toohello 클러스터가 될 수 있습니다.
2. 클러스터를 만드는 동안 클러스터 사용자 지정-추가 설정과 hello 클러스터 노드에 설치 될 사용자 지정 구성 요소를 지정할 수 있습니다.
3. 샘플-인기 있는 사용자 지정 구성 요소, Microsoft 등에 대 한 예제는 hello HDInsight 클러스터에서 이러한 구성 요소를 사용할 수 있는 방법을 제공할 수 있습니다. 이러한 샘플은 지원 없이 제공됩니다.

## <a name="develop-script-action-scripts"></a>스크립트 작업 스크립트 개발
[HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]을 참조하세요.

## <a name="see-also"></a>참고 항목
* [HDInsight에서 Hadoop 클러스터를 만들어] [ hdinsight-provision-cluster] 다른 사용자 지정 옵션을 사용 하 여 toocreate HDInsight 클러스터 하는 방법에 대해 설명 합니다.
* [HDInsight용 스크립트 작업 스크립트 개발][hdinsight-write-script]
* [HDInsight 클러스터에서 Spark 설치 및 사용][hdinsight-install-spark]
* [HDInsight 클러스터에서 R 설치 및 사용][hdinsight-install-r]
* [HDInsight 클러스터에 Solr 설치 및 사용](hdinsight-hadoop-solr-install.md)
* [HDInsight 클러스터에서 Giraph 설치 및 사용](hdinsight-hadoop-giraph-install.md)

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "클러스터를 만드는 동안의 단계"
