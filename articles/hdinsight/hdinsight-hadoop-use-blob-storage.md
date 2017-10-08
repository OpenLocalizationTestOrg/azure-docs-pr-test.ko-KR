---
title: "aaaQuery 데이터를 HDFS 호환 Azure 저장소-Azure HDInsight | Microsoft Docs"
description: "Tooquery 데이터를 Azure 저장소와 Azure 데이터 레이크 저장소 toostore 발생 하는 방법에 대해 알아봅니다 분석 합니다."
keywords: "Blob 저장소, HDFS, 구조적 데이터, 비구조적 데이터, Data Lake Store, Hadoop 입력, Hadoop 출력, Hadoop 저장소, HDFS 입력, HDFS 출력, HDFS 저장소, WASB Azure"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a>Azure HDInsight 클러스터에서 Azure Storage 사용

HDInsight 클러스터의 tooanalyze 데이터를 Azure 저장소, Azure 데이터 레이크 저장소 또는 둘 다에 hello 데이터를 저장할 수 있습니다. 저장소 옵션을 모두 사용자 데이터의 손실 없이 계산에 사용 되는 toosafely 삭제 HDInsight 클러스터를 설정 합니다.

Hadoop은 hello 기본 파일 시스템의 개념을 지원합니다. hello 기본 파일 시스템에는 기본 스키마와 기관 의미합니다. 상대 경로 사용 하는 tooresolve 수도 있습니다. Hello HDInsight 클러스터를 만드는 프로세스 동안 hello 기본 파일 시스템으로 Azure 저장소의 blob 컨테이너를 지정할 수 있습니다 하거나 HDInsight 3.5와 함께 선택할 수 있습니다 Azure 저장소 또는 Azure 데이터 레이크 저장소 몇 가지 예외와 함께 hello 기본 파일 시스템으로 합니다. 데이터 레이크 저장소를 사용 하 여 hello 기본 및 연결 된 저장소로의 지원 가능성 hello에 대 한 참조 [HDInsight 클러스터에 대 한 Availabilities](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters)합니다.

이 문서에서는 Azure Storage가 HDInsight 클러스터에서 작동하는 방식에 대해 알아봅니다. toolearn 데이터 레이크 저장소의 HDInsight 클러스터와 함께 작동 하는 방법 참조 [Azure HDInsight를 사용 하 여 Azure 데이터 레이크 저장소 클러스터](hdinsight-hadoop-use-data-lake-store.md)합니다. HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

Azure Storage는 HDInsight와 매끄럽게 통합되는 강력한 범용 저장소 솔루션입니다. HDInsight은 클러스터 hello에 대 한 blob 컨테이너를 Azure 저장소에 hello 기본 파일 시스템으로 사용할 수 있습니다. Hadoop 분산된 파일 시스템 (HDFS) 인터페이스를 통해 HDInsight의 구성 요소 중 일부만 hello blob으로 저장 하는 구조적 또는 비구조적 데이터를 직접 작동할 수 있습니다.

> [!WARNING]
> Azure Storage 계정을 만들 때 사용할 수 있는 몇 가지 옵션이 있습니다. HDInsight와 옵션에 대해 지원 되는 정보를 제공 하는 다음 표에 hello:
> 
> | 저장소 계정 유형 | 저장소 계층 | HDInsight에서 지원됨 |
> | ------- | ------- | ------- |
> | 범용 저장소 계정 | Standard | __예__ |
> | &nbsp; | Premium | 아니요 |
> | Blob Storage 계정 | 핫 | 아니요 |
> | &nbsp; | 쿨 | 아니요 |

비즈니스 데이터를 저장 하기 위한 hello 기본 blob 컨테이너를 사용 하는 것은 좋지 않습니다. 각 사용 tooreduce 후 hello 기본 blob 컨테이너를 삭제 합니다. 저장소 비용은 것이 좋습니다. 응용 프로그램 및 시스템 hello 기본 컨테이너를 포함 하는 참고 로그 합니다. Hello 컨테이너를 삭제 하기 전에 있는지 tooretrieve hello 로그를 확인 합니다.

여러 클러스터에 대해 하나의 Blob 컨테이너를 공유하는 것은 지원되지 않습니다.

## <a name="hdinsight-storage-architecture"></a>HDInsight 저장소 아키텍처
hello 다이어그램을 다음 hello Azure 저장소를 사용 하 여 HDInsight 저장소 아키텍처에 대 한 요약 보기를 제공 합니다.

![Hadoop 클러스터 HDFS API tooaccess hello를 사용 하 고 Blob 저장소의 데이터 및 구조화 되지 않은 데이터를 저장 합니다. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight 저장소 아키텍처")

HDInsight는 로컬 액세스 toohello 분산 파일 시스템 연결 toohello 계산 노드를 제공 합니다. 이 파일 시스템을 사용 하 여 액세스할 수 hello 정규화 된 URI, 예:

    hdfs://<namenodehost>/<path>

또한 HDInsight 있습니다 tooaccess 데이터를 Azure 저장소에 저장 됩니다. hello 구문은 다음과 같습니다.

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

다음은 HDInsight 클러스터와 Azure Storage 계정을 사용하는 경우 고려 사항입니다.

* **클러스터를 연결 된 tooa hello 저장소 계정에서 컨테이너:** hello 계정 이름 및 키에 연결 되어 hello 클러스터를 만드는 동안 저장할 수 있는 해당 컨테이너에 대 한 모든 권한을 toohello blob입니다.

* **공용 컨테이너 또는 되지 않은 저장소 계정에서 공용 blob 연결 tooa 클러스터:** hello 컨테이너의 toohello blob 읽기 전용 권한이 있어야 합니다.
  
  > [!NOTE]
  > 공용 컨테이너를 사용 하면 컨테이너 메타 데이터 가져오기 및 해당 컨테이너에서 사용 되는 모든 blob 목록을 tooget 있습니다. 공용 blob를 사용 하면 tooaccess hello blob hello 정확한 URL을 알고 있는 경우에 합니다. 자세한 내용은 참조 <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">액세스 toocontainers 및 blob 제한</a>합니다.
  > 
  > 
* **Tooa 클러스터를 연결 하지 않은 저장소 계정에 개인 컨테이너:** hello WebHCat 작업을 제출 하면 hello 저장소 계정을 정의 하지 않으면 hello 컨테이너에서 hello blob에 액세스할 수 없습니다. 이것은 문서 뒷부분에 설명되어 있습니다.

hello 생성 프로세스와 해당 키에 정의 된 hello 저장소 계정은 hello 클러스터 노드에서 %HADOOP_HOME%/conf/core-site.xml에 저장 됩니다. hello 기본 hdinsight 동작은 hello 코어 site.xml 파일에 정의 된 toouse hello 저장소 계정입니다. [Ambari](./hdinsight-hadoop-manage-ambari.md)를 사용하여 이 설정을 수정할 수 있습니다.

Hive, MapReduce, Hadoop 스트리밍 및 Pig를 비롯한 여러 WebHCat 작업은 저장소 계정 및 메타데이터 설명을 포함할 수 있습니다. (현재 메타데이터가 아닌 저장소 계정이 있는 Pig에서 작동합니다.) 자세한 내용은 [대체 저장소 계정 및 Metastore와 HDInsight 클러스터 사용](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx)을 참조하세요.

구조적 및 비구조적 데이터에 대한 Blob을 사용할 수 있습니다. Blob 컨테이너는 키/값 쌍으로 데이터를 저장하며, 디렉터리 계층 구조는 없습니다. Hello 슬래시 문자 (/) 내에서 사용할 수 있지만 hello 키 이름 toomake 파일이 디렉터리 구조에 저장 되어 처럼 것으로 표시 합니다. 예를 들어 Blob의 키 이름을 *input/log1.txt*로 지정할 수 있습니다. 더 실제 *입력* 디렉터리가 있는 했으나 인해 hello 키 이름에 슬래시 문자 hello toohello 상태에서 파일 경로의 hello 모양입니다.

## <a id="benefits"></a>Azure Storage의 이점
hello 암시 hello 계산 클러스터 hello 여기서 hello 고속 네트워크를 사용 하면 Azure 지역 내에서 저장소 계정 리소스 닫기 toohello 만들어집니다 hello 방식으로 공동 배치 계산 클러스터 및 저장소 리소스의 성능 비용 적어집니다. 계산 노드 hello에 대 한 효율적인 tooaccess hello Azure 저장소 내에서 데이터입니다.

관련 hello 데이터 HDFS 대신 Azure 저장소에 저장 된 다양 한 이점이 있습니다.

* **데이터를 다시 사용 및 공유:** HDFS에 hello 데이터는 hello 계산 클러스터 내 위치입니다. 액세스 toohello만 hello 응용 프로그램 계산 클러스터 HDFS Api를 사용 하 여 hello 데이터를 사용할 수 있습니다. hello HDFS Api 또는 hello 통해 hello Azure 저장소의에서 데이터를 액세스할 수 있습니다 [Blob 저장소 REST Api][blob-storage-restAPI]합니다. 따라서 응용 프로그램 (다른 HDInsight 클러스터 포함) 및 도구 집합 사용된 tooproduce 수 있으며 hello 데이터를 소비 됩니다.
* **데이터 보관:** 계산 toobe 사용자 데이터의 손실 없이 안전 하 게 삭제에 사용 되는 hello HDInsight 클러스터를 사용 하면 Azure 저장소에 데이터를 저장 합니다.
* **데이터 저장소 비용:** hello 장기 보다 가격이 더 비쌉니다 hello 비용 계산 클러스터의 Azure 저장소의 hello 비용 보다 높습니다. 때문에 Azure 저장소에 대 한 hello 데이터 저장에 대 한 DFS에 데이터를 저장 합니다. 또한 hello 데이터에 모든 계산 클러스터 생성에 대 한 다시 로드 toobe 없기 때문에 데이터 로드 비용 저장 됩니다.
* **탄력적 확장:** 있지만 HDFS 제공 스케일 아웃 파일 시스템으로, hello 눈금 hello 클러스터에 대해 만드는 노드 수에 의해 결정 됩니다. Hello 배율을 변경 hello 탄력적인 Azure 저장소에 자동으로 얻을 수 있는 기능을 크기 조정에 의존 하는 보다 더 복잡 한 프로세스가 될 수 있습니다.
* **지역에서 복제:** Azure Storage를 지역에서 복제할 수 있습니다. 이렇게 하면 지리적 복구 및 데이터 중복을 수 있지만 장애 조치 toohello 지리적으로 복제 된 위치에 성능에 심각한 영향을 받습니다와 그 추가 비용이 발생할 수 있습니다. 권장 하는 것은 toochoose hello 지리적 복제 현명 하 게 하 고 hello 추가 비용 가치가 hello 값 hello 데이터의 경우에 합니다.

특정 MapReduce 작업 및 패키지는 Azure 저장소에 실제로 toostore 않도록 중간 결과 만들 수 있습니다. 경우 toostore hello 데이터를 선택할 수 있다는 점에서 로컬 HDFS hello 합니다. 실제로 HDInsight는 Hive 작업 및 기타 프로세스에서 생성되는 이러한 중간 결과 중 일부에 DFS를 사용합니다.

> [!NOTE]
> 대부분의 HDFS 명령(예를 들어, <b>ls</b>, <b>copyFromLocal</b> 및 <b>mkdir</b>)은 여전히 예상대로 작동합니다. 와 같은 특정 toohello 네이티브 HDFS 구현 (즉, 참조 tooas DFS) 않은 명령만 hello <b>fschk</b> 및 <b>dfsadmin</b>, Azure 저장소의 다른 동작을 표시 합니다.
> 
> 

## <a name="create-blob-containers"></a>Blob 컨테이너 만들기
toouse blob을 먼저 만들어야는 [Azure 저장소 계정][azure-storage-create]합니다. 이 단계의 일부로 Azure 지역 hello 저장소 계정을 만든 위치를 지정 합니다. hello 클러스터와 hello 저장소 계정에서에서 호스팅되어야 hello 동일한 지역입니다. hello 하이브 metastore SQL Server 데이터베이스 및 SQL Server 데이터베이스에도 있어야 Oozie metastore hello 동일한 지역입니다.

될 때마다 Azure 저장소 계정에서 tooa 컨테이너를 만들면 각 blob에 속해 있습니다. 이 컨테이너는 HDInsight 외부에 생성된 기존 Blob일 수도 있고 HDInsight 클러스터용으로 생성된 컨테이너일 수도 있습니다.

hello 기본 Blob 컨테이너 작업 기록 로그 등 클러스터 관련 정보를 저장 합니다. 여러 HDInsight 클러스터의 기본 Blob 컨테이너를 공유하지 마세요. 이 경우 작업 기록이 손상될 수 있습니다. 클러스터 하 고 hello 기본 저장소 계정 대신 모든 클러스터의 배포에 지정 된 연결 된 저장소 계정에 공유 데이터를 저장 하는 각각에 대해 서로 다른 컨테이너 toouse 것이 좋습니다. 연결된 저장소 계정에 대한 자세한 내용은 [HDInsight 클러스터 만들기][hdinsight-creation]를 참조하세요. 그러나 hello 원래 HDInsight 클러스터 삭제 한 후 기본 저장소 컨테이너를 사용할 수 있습니다. HBase 클러스터에 대 한 실제로 여 유지할 수 있습니다 hello HBase 테이블 스키마 및 데이터는 삭제 된 HBase 클러스터에서 사용 되는 hello 기본 blob 컨테이너를 사용 하 여 새 HBase 클러스터를 만듭니다.

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a>Hello Azure 포털을 사용 하 여
Hello 포털에서에서 하는 HDInsight 클러스터를 만들 때는 hello 옵션 (아래와 같이) tooprovide hello 저장소 계정 세부 정보를 수 있습니다. 사용할지 여부는 추가 저장소 계정 hello 클러스터와 연결 된 및 데이터 레이크 저장소 또는 다른 Azure 저장소 blob 저장소를 추가 하는 hello로 중에서 선택할 경우 지정할 수 있습니다.

![HDInsight Hadoop 만들기 데이터 원본](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> 추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.


### <a name="use-azure-powershell"></a>Azure PowerShell 사용
경우 있습니다 [설치 하 고 Azure PowerShell을 구성][powershell-install], 저장소 계정 및 컨테이너에서 hello Azure PowerShell 프롬프트 toocreate 다음 hello를 사용할 수 있습니다.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a>Azure CLI 사용

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

있는 경우 [설치 및 구성 hello Azure CLI](../cli-install-nodejs.md), hello 다음 명령을 사용 하는 tooa 저장소 계정 및 컨테이너 될 수 있습니다.

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> hello `--type` 매개 변수는 hello 저장소 계정이 복제 방법을 나타냅니다. 자세한 내용은 [Azure Storage 복제](../storage/storage-redundancy.md)를 참조하세요. ZRS에서 페이지 Blob, 파일, 테이블 또는 큐를 지원하지 않으므로 ZRS를 사용하지 마세요.
> 
> 

Hello 저장소 계정에서 생성 된 증명된 toospecify hello 지리적인 지역의 됩니다. Hello에 hello 저장소 계정을 만들어야 합니다. 동일한 지역에 HDInsight 클러스터를 만드는 방법에 있습니다.

Hello 저장소 계정이 만들어지면 명령 tooretrieve hello 저장소 계정 키를 다음 hello를 사용 합니다.

    azure storage account keys list <storageaccountname>

컨테이너를 toocreate hello 다음 명령을 사용 합니다.

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a>Azure Storage에서 파일 주소 지정
HDInsight에서 Azure 저장소의 파일에 액세스 하기 위한 URI 체계 hello은입니다.

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

암호화 되지 않은 액세스를 제공 하는 hello URI 체계 (hello로 *wasb:* 접두사) 및 SSL 암호화 액세스 (으로 *wasbs*). 사용 하는 것이 좋습니다 *wasbs* 내에 있는 데이터를 액세스 하는 Azure에서 동일한 지역 hello 하는 경우에 가능 합니다.

hello &lt;BlobStorageContainerName&gt; hello blob 저장소 컨테이너에 Azure의 hello 이름을 식별 합니다.
hello &lt;StorageAccountName&gt; hello Azure 저장소 계정 이름을 식별 합니다. FQDN(정규화된 도메인 이름)이 필요합니다.

모두 &lt;BlobStorageContainerName&gt; 나 &lt;StorageAccountName&gt; 지정 hello 기본 파일 시스템 사용 됩니다. Hello 기본 파일 시스템에 있는 hello 파일에 대 한 상대 경로 또는 절대 경로 사용할 수 있습니다. 예를 들어 hello *mapreduce hadoop-examples.jar* HDInsight 클러스터와 함께 제공 되는 파일에는 hello 다음 중 하나를 사용 하 여 참조 된 tooby 될 수 있습니다.

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> hello 파일 이름이 <i>hadoop-examples.jar</i> 버전 2.1 및 1.6는 HDInsight 클러스터에 있습니다.
> 
> 

hello &lt;경로&gt; hello 파일 또는 디렉터리 HDFS 경로 이름입니다. Azure Storage의 컨테이너는 단지 키-값 저장소이므로 실제 계층적 파일 시스템이 없습니다. Blob 키 내부의 슬래쉬 문자(/)는 디렉터리 구분기호로 해석됩니다. 에 대 한 blob 이름 예를 들어 hello *mapreduce hadoop-examples.jar* 됩니다.

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> HDInsight 외부 blob를 사용할 때 대부분의 유틸리티 및 하지 않는 hello WASB 형식을 인식 대신와 같은 기본 경로 형식으로 예상 되 `example/jars/hadoop-mapreduce-examples.jar`합니다.
> 
> 

## <a name="access-blobs"></a>Blob 액세스 


### <a name="access-blobs-using-azure-powershell"></a> Azure PowerShell 사용
> [!NOTE]
> 이 섹션의 hello 명령은 blob에 저장 된 PowerShell tooaccess 데이터를 사용 하 여 기본 예제를 제공 합니다. HDInsight를 사용 하기 위한 사용자 지정 된 보다 복잡 예제 참조 hello [HDInsight 도구](https://github.com/Blackmist/hdinsight-tools)합니다.
> 
> 

사용 하 여 hello 다음 명령 toolist hello blob 관련 cmdlet을 사용할 수 있습니다.

    Get-Command *blob*

![Blob 관련 PowerShell cmdlet의 목록입니다.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a>파일 업로드
참조 [데이터 tooHDInsight 업로드][hdinsight-upload-data]합니다.

#### <a name="download-files"></a>파일 다운로드
hello 다음 스크립트를 다운로드 블록 blob toohello 현재 폴더 합니다. Hello 스크립트를 실행 하기 전에 쓰기 권한이 있는 hello 디렉터리 tooa 폴더를 변경 합니다.

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

Hello 리소스 그룹 이름 및 hello 클러스터 이름을 제공 하 hello 코드 다음에 사용할 수 있습니다.

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a>파일 삭제
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a>파일 나열
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a>정의되지 않은 저장소 계정을 사용하여 Hive 쿼리 실행
이 예제에서는 toolist 하는 동안 정의 되지 않은 저장소 계정에서 폴더를 만드는 프로세스 hello 하는 방법을 보여 줍니다.
$clusterName = "<HDInsightClusterName>"

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a>Azure CLI 사용
다음 명령 toolist hello blob 관련 명령을 hello를 사용 합니다.

    azure storage blob

**Azure CLI tooupload 파일 사용의 예**

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toodownload 파일 사용의 예**

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toodelete 파일 사용의 예**

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

**Azure CLI toolist 파일 사용의 예**

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a>추가 저장소 계정 사용

HDInsight 클러스터를 만드는 동안 함께 tooassociate 원하는 hello Azure 저장소 계정을 지정 합니다. 또한 toothis 저장소 계정을 추가할 수 있습니다 hello에서 추가 저장소 계정을 동일한 Azure 구독 또는 hello 만드는 프로세스 동안 또는 클러스터를 만든 후에 서로 다른 Azure 구독. 저장소 계정 추가에 대한 지침은 [HDInsight 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

> [!WARNING]
> 추가 저장소 계정을 사용 하 여 hello HDInsight 클러스터와 다른 위치에서 지원 되지 않습니다.

## <a name="next-steps"></a>다음 단계
이 문서에서는 방법에 대해 배웠습니다 toouse HDFS 호환 HDInsight와 메트릭을 제공 합니다. 이렇게 하면 구조화 되지 않은 데이터 및 데이터 취득 솔루션 및 구성 저장 hello 내부의 HDInsight toounlock hello 정보를 사용 하 여 보관 toobuild 확장 가능 하 고 장기, 있습니다.

자세한 내용은 다음을 참조하세요.

* [Azure HDInsight 시작][hdinsight-get-started]
* [Azure Data Lake Store 시작](../data-lake-store/data-lake-store-get-started-portal.md)
* [데이터 tooHDInsight 업로드][hdinsight-upload-data]
* [HDInsight에서 Hive 사용][hdinsight-use-hive]
* [HDInsight에서 Pig 사용][hdinsight-use-pig]
* [HDInsight와 Azure 저장소 공유 액세스 서명 toorestrict 액세스 toodata 사용][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
