---
title: "HDInsight에 대 한 aaaMigrate tooAzure 리소스 관리자 도구 | Microsoft Docs"
description: "HDInsight 클러스터에 대 한 toomigrate tooAzure 리소스 관리자 개발 도구 하는 방법"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a>HDInsight 클러스터에 대 한 마이그레이션 tooAzure 리소스 관리자 기반 개발 도구

HDInsight에서는 HDInsight용 ASM(Azure 서비스 관리자) 기반 도구를 지원하지 않습니다. 사용 된 Azure PowerShell, Azure CLI 또는 hello HDInsight.NET SDK toowork HDInsight 클러스터를 모르는 경우 hello Azure 리소스 관리자 ARM 기반 PowerShell, CLI 및 앞으로.NET SDK 버전 toouse 것이 좋습니다. 이 문서는 방법에 대 한 포인터를 제공 toomigrate toohello 새로운 ARM 기반 접근 방식입니다. 해당 되는 경우이 문서의 링크 HDInsight에 대 한 hello ASM 및 ARM 방법 hello 차이점 아웃 합니다.

> [!IMPORTANT]
> ASM에 대 한 hello 지원 기반 CLI, PowerShell 및.NET SDK 중단 됩니다. **2017 년 1 월 1**합니다.
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a>마이그레이션 Azure CLI tooAzure 리소스 관리자
hello Azure CLI tooAzure 리소스 관리자 (ARM) 모드를; 이전 설치에서 업그레이드 하는 경우가 아니면 이제 기본적으로 이 경우 toouse hello를 할 수 있습니다 `azure config mode arm` 명령 tooswitch tooARM 모드입니다.

Azure 서비스 관리 (ASM)를 사용 하 여 HDInsight toowork 제공 Azure CLI 해당 hello ARM;를 사용 하는 경우 동일한 hello는 hello 기본 명령 그러나 일부 매개 변수 및 스위치 새 이름을 없고 많은 새로운 매개 변수가 사용할 수 있는 ARM를 사용 하는 경우. 예를 들어 이제 사용할 수 있습니다 `azure hdinsight cluster create` toospecify hello Azure 가상 네트워크를 클러스터에서를 만들지 또는 Hive 및 Oozie metastore 정보입니다.

Azure Resource Manager를 통한 HDInsight를 사용하는 기본 명령은 다음과 같습니다.

* `azure hdinsight cluster create` - 새 HDInsight 클러스터를 만듭니다.
* `azure hdinsight cluster delete` - 새 HDInsight 클러스터를 삭제합니다.
* `azure hdinsight cluster show` - 기존 클러스터에 대한 정보를 표시합니다.
* `azure hdinsight cluster list` - Azure 구독에 대한 HDInsight 클러스터를 나열합니다.

사용 하 여 hello `-h` tooinspect hello 매개 변수 및 명령에 따라 사용할 수 있는 스위치를 전환 합니다.

### <a name="new-commands"></a>새 명령
Azure Resource Manager로 사용할 수 있는 새 명령은 다음과 같습니다.

* `azure hdinsight cluster resize`-동적으로 변경 내용을 hello hello 클러스터의 작업자 노드 수
* `azure hdinsight cluster enable-http-access`-HTTPs 액세스 toohello 클러스터 (에 기본적으로)
* `azure hdinsight cluster disable-http-access`-HTTPs 액세스 toohello 클러스터를 사용 하지 않도록 설정
* `azure hdinsight script-action` - 클러스터에서 스크립트 작업을 만들기/관리하기 위한 명령을 제공합니다.
* `azure hdinsight config`-hello로 사용 될 수 있는 구성 파일을 만드는 명령을 제공 `hdinsight cluster create` 명령 tooprovide 구성 정보입니다.

### <a name="deprecated-commands"></a>사용되지 않는 명령
Hello를 사용 하는 경우 `azure hdinsight job` 명령 toosubmit 작업 tooyour HDInsight 클러스터를 사용할 수 없는 hello ARM 명령입니다. 스크립트에서 전송 작업 tooHDInsight tooprogrammatically 해야 할 경우 hello HDInsight에서 제공 하는 REST Api를 대신 사용 해야 합니다. REST Api를 사용 하 여 작업 등록에 대 한 자세한 내용은 다음 문서는 hello를 참조 하세요.

* [cURL을 사용하여 HDInsight에서 Hadoop과 MapReduce 작업 실행](hdinsight-hadoop-use-mapreduce-curl.md)
* [cURL을 사용하여 HDInsight에서 Hadoop과 Hive 쿼리 실행](hdinsight-hadoop-use-hive-curl.md)
* [cURL을 사용하여 HDInsight에서 Hadoop과 Pig 작업 실행](hdinsight-hadoop-use-pig-curl.md)

다른 방법으로 toorun MapReduce 대 한 자세한 내용은, Hive 및 Pig 대화형으로 참조 하십시오 [HDInsight에서 Hadoop으로 사용 하 여 MapReduce](hdinsight-use-mapreduce.md), [HDInsight에서 Hadoop으로 사용 하 여 하이브](hdinsight-use-hive.md), 및 [Pig에서 Hadoop으로 HDInsight](hdinsight-use-pig.md)합니다.

### <a name="examples"></a>예
**클러스터 만들기**

* 이전 명령(ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`
* 새 명령(ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`

**클러스터 삭제**

* 이전 명령(ASM) - `azure hdinsight cluster delete myhdicluster`
* 새 명령(ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`

**클러스터 나열**

* 이전 명령(ASM) - `azure hdinsight cluster list`
* 새 명령(ARM) - `azure hdinsight cluster list`

> [!NOTE]
> 리소스 그룹을 사용 하 여 hello 지정 hello 목록 명령에 대 한 `-g` hello 지정 된 리소스 그룹의 hello 클러스터만을 반환 합니다.
> 
> 

**클러스터 정보 표시**

* 이전 명령(ASM) - `azure hdinsight cluster show myhdicluster`
* 새 명령(ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a>Azure PowerShell tooAzure 리소스 관리자가 마이그레이션
hello Azure 리소스 관리자 (ARM) 모드에서 Azure PowerShell에 대 한 hello 일반 정보에서 찾을 수 있습니다 [Azure PowerShell 사용 하 여 Azure 리소스 관리자와](../powershell-azure-resource-manager.md)합니다.

hello Azure PowerShell ARM cmdlet hello ASM cmdlet와 함께 설치 될 수 있습니다. hello 두 가지 모드에서 hello cmdlet은 이름으로 구분할 수 있습니다.  hello ARM 모드는 *AzureRmHDInsight* 너무 비교 hello cmdlet 이름에서*AzureHDInsight* hello ASM 모드에서입니다.  예를 들면 *New-AzureRmHDInsightCluster* 및 *New-AzureHDInsightCluster*가 있습니다. 매개 변수 및 스위치에는 새 이름이 있을 수 있고 ARM을 사용하는 경우 많은 새 매개 변수를 사용할 수 있습니다.  예를 들어 일부 cmdlet에는 *-ResourceGroupName*이라는 새 스위치가 필요합니다. 

Hello HDInsight cmdlet을 사용 하려면 먼저 tooyour Azure 계정을 연결 하 고 새 리소스 그룹을 생성 해야 합니다.

* Login-AzureRmAccount 또는 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)입니다. [Azure Resource Manager를 사용하여 서비스 사용자 인증](../azure-resource-manager/resource-group-authenticate-service-principal.md)
* [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a>이름이 바뀐 cmdlet
toolist hello Windows PowerShell 콘솔에서 ASM HDInsight cmdlet:

    help *azurermhdinsight*

hello 다음 표에 hello ASM cmdlet 및 hello ARM 모드에 해당 이름을 있습니다.

| ASM cmdlet | ARM cmdlet |
| --- | --- |
| Add-AzureHDInsightConfigValues |[Add-AzureRmHDInsightConfigValues](https://msdn.microsoft.com/library/mt603530.aspx) |
| Add-AzureHDInsightMetastore |[Add-AzureRmHDInsightMetastore](https://msdn.microsoft.com/library/mt603670.aspx) |
| Add-AzureHDInsightScriptAction |[Add-AzureRmHDInsightScriptAction](https://msdn.microsoft.com/library/mt603527.aspx) |
| Add-AzureHDInsightStorage |[Add-AzureRmHDInsightStorage](https://msdn.microsoft.com/library/mt619445.aspx) |
| Get-AzureHDInsightCluster |[Get-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619371.aspx) |
| Get-AzureHDInsightJob |[Get-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603590.aspx) |
| Get-AzureHDInsightJobOutput |[Get-AzureRmHDInsightJobOutput](https://msdn.microsoft.com/library/mt603793.aspx) |
| Get-AzureHDInsightProperties |[Get-AzureRmHDInsightProperties](https://msdn.microsoft.com/library/mt603546.aspx) |
| Grant-AzureHDInsightHttpServicesAccess |[Grant-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619407.aspx) |
| Grant-AzureHdinsightRdpAccess |[Grant-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603717.aspx) |
| Invoke-AzureHDInsightHiveJob |[Invoke-AzureRmHDInsightHiveJob](https://msdn.microsoft.com/library/mt603593.aspx) |
| New-AzureHDInsightCluster |[New-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619331.aspx) |
| New-AzureHDInsightClusterConfig |[New-AzureRmHDInsightClusterConfig](https://msdn.microsoft.com/library/mt603700.aspx) |
| New-AzureHDInsightHiveJobDefinition |[New-AzureRmHDInsightHiveJobDefinition](https://msdn.microsoft.com/library/mt619448.aspx) |
| New-AzureHDInsightMapReduceJobDefinition |[New-AzureRmHDInsightMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| New-AzureHDInsightPigJobDefinition |[New-AzureRmHDInsightPigJobDefinition](https://msdn.microsoft.com/library/mt603671.aspx) |
| New-AzureHDInsightSqoopJobDefinition |[New-AzureRmHDInsightSqoopJobDefinition](https://msdn.microsoft.com/library/mt608551.aspx) |
| New-AzureHDInsightStreamingMapReduceJobDefinition |[New-AzureRmHDInsightStreamingMapReduceJobDefinition](https://msdn.microsoft.com/library/mt603626.aspx) |
| Remove-AzureHDInsightCluster |[Remove-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619431.aspx) |
| Revoke-AzureHDInsightHttpServicesAccess |[Revoke-AzureRmHDInsightHttpServicesAccess](https://msdn.microsoft.com/library/mt619375.aspx) |
| Revoke-AzureHdinsightRdpAccess |[Revoke-AzureRmHDInsightRdpServicesAccess](https://msdn.microsoft.com/library/mt603523.aspx) |
| Set-AzureHDInsightClusterSize |[Set-AzureRmHDInsightClusterSize](https://msdn.microsoft.com/library/mt603513.aspx) |
| Set-AzureHDInsightDefaultStorage |[Set-AzureRmHDInsightDefaultStorage](https://msdn.microsoft.com/library/mt603486.aspx) |
| Start-AzureHDInsightJob |[Start-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603798.aspx) |
| Stop-AzureHDInsightJob |[Stop-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt619424.aspx) |
| Use-AzureHDInsightCluster |[Use-AzureRmHDInsightCluster](https://msdn.microsoft.com/library/mt619442.aspx) |
| Wait-AzureHDInsightJob |[Wait-AzureRmHDInsightJob](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a>새 cmdlet
hello 다음 hello 에서만 hello ARM 모드에서 사용할 수 있는 새로운 cmdlet은입니다. 

**cmdlet 관련 스크립트 작업:**

* **Get AzureRmHDInsightPersistedScriptAction**: 가져옵니다 hello 클러스터에 대 한 스크립트 작업을 유지 하 고 시간 순서로 나열 또는 지정 된 지속형된 스크립트 동작에 대 한 세부 정보를 가져옵니다. 
* **Get AzureRmHDInsightScriptActionHistory**: 클러스터에 대 한 hello 스크립트 동작 기록을 가져옵니다 및 시간 순서 대로 나열 하거나 이전에 실행된 한 스크립트 작업의 세부 정보를 가져옵니다. 
* **Remove-AzureRmHDInsightPersistedScriptAction**: HDInsight 클러스터에서 지속형 스크립트 동작을 제거합니다.
* **집합 AzureRmHDInsightPersistedScriptAction**: 이전에 실행된 한 스크립트 작업 toobe 지속형된 스크립트 동작을 설정 합니다.
* **제출 AzureRmHDInsightScriptAction**: 새 스크립트 동작이 tooan Azure HDInsight 클러스터를 전송 합니다. 

추가 사용 정보는 [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](hdinsight-hadoop-customize-cluster-linux.md)을 참조하세요.

**cmdlet 관련 클러스터 ID:**

* **추가 AzureRmHDInsightClusterIdentity**: hello HDInsight 클러스터에 액세스할 수 있는 Azure 데이터 레이크 저장소 클러스터 id tooa 클러스터 구성 개체를 추가 합니다. [Azure PowerShell을 사용하여 Data Lake 저장소로 HDInsight 클러스터 만들기](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)를 참조하세요.

### <a name="examples"></a>예
**클러스터 만들기**

이전 명령(ASM): 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

새 명령(ARM):

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


**클러스터 삭제**

이전 명령(ASM):

    Remove-AzureHDInsightCluster -name $clusterName 

새 명령(ARM):

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

**클러스터 나열**

이전 명령(ASM):

    Get-AzureHDInsightCluster

새 명령(ARM):

    Get-AzureRmHDInsightCluster 

**클러스터 표시**

이전 명령(ASM):

    Get-AzureHDInsightCluster -Name $clusterName

새 명령(ARM):

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a>다른 샘플
* [HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [Hive 작업 제출](hdinsight-hadoop-use-hive-powershell.md)
* [Pig 작업 제출](hdinsight-hadoop-use-pig-powershell.md)
* [Sqoop 작업 제출](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a>마이그레이션 toohello ARM 기반 HDInsight.NET SDK
Azure 서비스 관리-기반 hello [(ASM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) 는 이제 사용 되지 않습니다. 것이 좋습니다 toouse는 Azure 리소스 관리 기반 hello [(ARM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)합니다. hello 다음 ASM 기반 HDInsight 패키지 되지 않습니다.

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

이 섹션에서는 포인터 toomore 정보는 방법에 특정 작업을 사용 하 여 hello ARM 기반 SDK tooperform 합니다.

| 방법... ARM 기반 HDInsight SDK hello를 사용 하 여 | 링크 |
| --- | --- |
| .NET SDK를 사용하여 HDInsight 클러스터 만들기 |[.NET SDK를 사용하여 HDInsight 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |
| .NET SDK와 스크립트 작업을 사용하여 클러스터 사용자 지정 |[스크립트 작업을 사용하여 HDInsight Linux 클러스터 사용자 지정](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action) |
| .NET SDK와 Azure Active Directory를 사용하여 대화형으로 응용 프로그램 인증 |[.NET SDK를 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-dotnet-sdk.md)을 참조하세요. 이 문서에서 코드 조각 hello hello 대화형 인증 접근 방법을 사용합니다. |
| .NET SDK와 Azure Active Directory를 사용하여 비대화형으로 응용 프로그램 인증 |[HDInsight에 대한 비대화형 응용 프로그램 만들기](hdinsight-create-non-interactive-authentication-dotnet-applications.md) |
| .NET SDK를 사용하여 Hive 작업 제출 |[Hive 작업 제출](hdinsight-hadoop-use-hive-dotnet-sdk.md) |
| .NET SDK를 사용하여 Pig 작업 제출 |[Pig 작업 제출](hdinsight-hadoop-use-pig-dotnet-sdk.md) |
| .NET SDK를 사용하여 Sqoop 작업 제출 |[Sqoop 작업 제출](hdinsight-hadoop-use-sqoop-dotnet-sdk.md) |
| .NET SDK를 사용하여 HDInsight 클러스터 나열 |[HDInsight 클러스터 나열](hdinsight-administer-use-dotnet-sdk.md#list-clusters) |
| .NET SDK를 사용하여 HDInsight 클러스터 크기 조정 |[HDInsight 클러스터 크기 조정](hdinsight-administer-use-dotnet-sdk.md#scale-clusters) |
| Grant/revoke access tooHDInsight.NET SDK를 사용 하는 클러스터 |참조 [Grant/revoke access tooHDInsight 클러스터](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access) |
| .NET SDK를 사용하여 HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트 |[HDInsight 클러스터에 대한 HTTP 사용자 자격 증명 업데이트](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials) |
| .NET SDK를 사용 하 여 HDInsight 클러스터에 대 한 hello 기본 저장소 계정 찾기 |참조 [hello 기본 저장소 계정이 HDInsight 클러스터에 대 한 찾기](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account) |
| .NET SDK를 사용하여 HDInsight 클러스터 삭제 |[HDInsight 클러스터 삭제](hdinsight-administer-use-dotnet-sdk.md#delete-clusters) |

### <a name="examples"></a>예
다음은 작업을 하는 방법을 보여 주는 예 hello ARM 기반 SDK에 대 한 hello ASM 기반 SDK 및 해당 하는 코드 조각 hello 사용 하 여 수행 합니다.

**클러스터 CRUD 클라이언트 만들기**

* 이전 명령(ASM)
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* 새 명령(ARM)(서비스 주체 권한 부여)
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* 새 명령(ARM)(사용자 권한 부여)
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

**클러스터 만들기**

* 이전 명령(ASM)
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* 새 명령(ARM)
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

**HTTP 액세스 사용**

* 이전 명령(ASM)
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* 새 명령(ARM)
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

**클러스터 삭제**

* 이전 명령(ASM)
  
        client.DeleteCluster(dnsName);
* 새 명령(ARM)
  
        client.Clusters.Delete(resourceGroup, dnsname);

