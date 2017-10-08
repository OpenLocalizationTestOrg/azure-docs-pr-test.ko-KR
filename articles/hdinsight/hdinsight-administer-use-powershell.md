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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Azure PowerShell을 사용하여 HDInsight의 Hadoop 클러스터 관리
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell은 toocontrol를 사용 하 고 Azure에서 작업의 hello 배포 및 관리를 자동화할 수 있는 강력한 스크립팅 환경입니다. 이 문서에서는 Windows PowerShell의 hello 통해 로컬 Azure PowerShell 콘솔을 사용 하 여 Azure HDInsight의 Hadoop 클러스터 toomanage 사용 하는 방법을 배웁니다. Hello 목록이 hello HDInsight PowerShell cmdlet 참조 하십시오. [HDInsight cmdlet 참조][hdinsight-powershell-reference]합니다.

**필수 구성 요소**

이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)을 참조하세요.

## <a name="install-azure-powershell"></a>Azure PowerShell 설치
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Azure PowerShell 버전 0.9x를 설치한 경우 최신 버전을 설치하기 전에 제거해야 합니다.

PowerShell을 설치 하는 hello의 toocheck hello 버전:

    Get-Module *azure*

toouninstall hello 이전 버전을 hello 제어판의 프로그램 및 기능을 실행 합니다.

## <a name="create-clusters"></a>클러스터 만들기
[Azure PowerShell을 사용하여 HDInsight에서 Linux 기반 클러스터 만들기](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>클러스터 나열
Hello 현재 구독에 다음 명령을 toolist hello 모든 클러스터를 사용 합니다.

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>클러스터 표시
다음 명령은 tooshow 세부 정보 hello 현재 구독에는 특정 클러스터의 hello를 사용 합니다.

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>클러스터 삭제
다음 명령은 toodelete 클러스터 hello를 사용 합니다.

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

또한 hello 클러스터를 포함 하는 hello 리소스 그룹을 제거 하 여 클러스터를 삭제할 수 있습니다. 하십시오 note, hello 그룹의에서 모든 리소스 hello hello 기본 저장소 계정을 포함 하 여 삭제 합니다.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>클러스터 크기 조정
hello 클러스터 기능을 확장 하면 toochange hello toore 필요 없이 Azure HDInsight에서 실행 되는 클러스터에서 사용 하는 작업자 노드 수-hello 클러스터를 만듭니다.

> [!NOTE]
> HDInsight 버전 3.1.3 이상을 사용하는 클러스터만 지원됩니다. 클러스터의 hello 버전을 잘 모를 경우 hello 속성 페이지를 확인할 수 있습니다.  [클러스터 나열 및 표시](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)를 참조하세요.
>
>

hello HDInsight에서 지원 되는 클러스터의 각 형식에 대 한 데이터 노드 수를 변경 하는 hello 미치는 영향:

* Hadoop은

    원활 하 게 hello 보류 중 또는 실행 중인 작업이 모두 영향을 주지 않고 실행 되는 Hadoop 클러스터의 작업자 노드 수를 늘릴 수 있습니다. Hello 작업이 진행 중인 동안에 새 작업을 제출할 수 있습니다. 크기 조정 작업의 오류는 hello 클러스터는 항상를 작동 상태로 남아 있도록 정상적으로 처리 됩니다.

    Hadoop 클러스터는 hello 데이터 노드 수를 줄여 규모 축소, hello 클러스터의 hello 서비스 중 일부를 다시 시작 됩니다. 이렇게 하면 실행 중인 모든와 hello hello 크기 조정 작업이 완료 될 때 작업 toofail 보류 중. 그러나 hello 작업이 완료 되 면 hello 작업을 다시 전송할을 수 있습니다.
* HBase

    원활 하 게 추가 하거나 실행 하는 동안 노드 tooyour HBase 클러스터를 제거할 수 있습니다. 지역 서버는 hello 크기 조정 작업을 완료 하는 몇 분 안에 자동으로 균형이 조정 됩니다. 그러나 명령을 명령 프롬프트 창에서 다음 실행 중인 hello와 클러스터의 헤드 노드에 toohello에 로그인 하 여 hello 지역 서버를 수동으로 분산 시킬 수 있습니다 있습니다.

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    원활 하 게 추가 하거나 실행 하는 동안 데이터 노드 tooyour Storm 클러스터를 제거할 수 있습니다. 하지만 hello 크기 조정 작업을 성공적으로 완료 한 후 toorebalance hello 토폴로지를 해야 합니다.

    다음 두 가지 방법으로 사용하여 균형을 조정할 수 있습니다.

  * Storm 웹 UI
  * 명령줄 인터페이스(CLI) 도구

    Toohello를 참조 하십시오 [Apache Storm 설명서](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) 자세한 세부 정보에 대 한 합니다.

    hello 스톰 웹 UI hello HDInsight 클러스터에서 제공 됩니다.

    ![HDInsight Storm 규모 균형 재조정](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    다음은 예제 어떻게 toouse hello CLI 명령을 toorebalance hello 스톰 토폴로지:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

toochange hello hello 클라이언트 컴퓨터에서 다음 명령을 실행 하는 Azure PowerShell을 사용 하 여 Hadoop 클러스터 크기:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>액세스 권한 부여/해지
HDInsight 클러스터에는 HTTP 웹 서비스 (모든 이러한 서비스는 RESTful 끝점)를 수행 하는 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

이러한 서비스에는 기본적으로 액세스 권한이 부여됩니다. 있습니다 수 revoke/hello 액세스를 허용 합니다. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

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
> Hello 액세스 권한을 부여/취소를 하 여 hello 클러스터 사용자 이름 및 암호를 설정 합니다.
>
>

이 hello 포털을 통해 수행할 수도 있습니다. 참조 [관리할 HDInsight를 사용 하 여 Azure 포털 hello][hdinsight-admin-portal]합니다.

## <a name="update-http-user-credentials"></a>HTTP 사용자 자격 증명 업데이트
동일한 hello와 프로시저 [Grant/revoke HTTP 액세스](#grant/revoke-access)합니다. Hello 클러스터 부여 된 경우에 hello HTTP 액세스를 먼저 취소 해야 있습니다.  한 다음 새 HTTP 사용자 자격 증명을 사용 하 여 hello 액세스 권한을 부여 합니다.

## <a name="find-hello-default-storage-account"></a>Hello 기본 저장소 계정 찾기
Powershell 스크립트 뒤 hello tooget hello 기본 저장소 계정 이름 및 클러스터에 대 한 기본 저장소 계정 키를 hello 방법을 보여 줍니다.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Hello 리소스 그룹 찾기
Hello 리소스 관리자 모드에서는 각 HDInsight 클러스터 tooan Azure 리소스 그룹을 속해 있습니다.  toofind hello 리소스 그룹:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>작업 제출
**toosubmit MapReduce 작업**

[Windows 기반 HDInsight에서 Hadoop MapReduce 샘플 실행](hdinsight-run-samples.md)을 참조하세요.

**toosubmit 하이브 작업**

[PowerShell을 사용하여 Hive 쿼리 실행](hdinsight-hadoop-use-hive-powershell.md)을 참조하세요.

**toosubmit Pig 작업**

[PowerShell을 사용하여 Pig 작업 실행](hdinsight-hadoop-use-pig-powershell.md)을 참조하세요.

**toosubmit Sqoop 작업**

[HDInsight와 함께 Sqoop 사용](hdinsight-use-sqoop.md)을 참조하세요.

**toosubmit Oozie 작업**

참조 [Hadoop toodefine 및 HDInsight에서 워크플로 실행 사용 Oozie](hdinsight-use-oozie.md)합니다.

## <a name="upload-data-tooazure-blob-storage"></a>데이터 tooAzure Blob 저장소에 업로드
참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.

## <a name="see-also"></a>참고 항목
* [HDInsight Cmdlet 참조 설명서][hdinsight-powershell-reference]
* [HDInsight hello Azure 포털을 사용 하 여 관리][hdinsight-admin-portal]
* [명령줄 인터페이스를 사용하여 HDInsight 관리][hdinsight-admin-cli]
* [HDInsight 클러스터 만들기][hdinsight-provision]
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [프로그래밍 방식으로 Hadoop 작업 제출][hdinsight-submit-jobs]
* [Azure HDInsight 시작][hdinsight-get-started]

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
