---
title: "Azure HDInsight에서 Hadoop으로 데이터 레이크 저장소 aaaUse | Microsoft Docs"
description: "Tooquery 및 데이터를 Azure 데이터 레이크 저장소 toostore 발생 하는 방법에 대해 알아봅니다 분석 합니다."
keywords: "Blob Storage, hdfs, 구조화된 데이터, 구조화되지 않은 데이터, Data Lake Store"
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Azure HDInsight 클러스터에 Data Lake Store 사용

HDInsight 클러스터의 tooanalyze 데이터를 저장할 수 있습니다 hello 데이터 중 하나에서 [Azure 저장소](../storage/common/storage-introduction.md), [Azure 데이터 레이크 저장소](../data-lake-store/data-lake-store-overview.md), 또는 둘 다 합니다. 저장소 옵션을 모두 사용자 데이터의 손실 없이 계산에 사용 되는 toosafely 삭제 HDInsight 클러스터를 설정 합니다.

이 문서에서는 Data Lake Store가 HDInsight 클러스터에서 작동하는 방식에 대해 알아봅니다. toolearn HDInsight 클러스터와 함께 작동 하는 Azure 저장소 참조 [사용 하 여 Azure 저장소와 Azure HDInsight 클러스터](hdinsight-hadoop-use-blob-storage.md)합니다. HDInsight 클러스터를 만드는 방법에 대한 자세한 내용은 [HDInsight에서 Hadoop 클러스터 만들기](hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요.

> [!NOTE]
> Data Lake Store는 항상 보안 채널을 통해 액세스되기 때문에 `adls` 파일 시스템 구성표 이름이 없습니다. 항상 `adl`을 사용합니다.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>HDInsight 클러스터에 대한 가용성

Hadoop은 hello 기본 파일 시스템의 개념을 지원합니다. hello 기본 파일 시스템에는 기본 스키마와 기관 의미합니다. 상대 경로 사용 하는 tooresolve 수도 있습니다. Hello HDInsight 클러스터를 만드는 프로세스 동안 hello 기본 파일 시스템으로 Azure 저장소의 blob 컨테이너를 지정할 수 있습니다 또는 HDInsight 3.5 및 최신 버전을 선택할 수 있습니다 Azure 저장소 또는 Azure 데이터 레이크 저장소와 함께 hello 기본 파일 시스템으로는 몇 가지 예외가 있습니다. 

HDInsight 클러스터는 Data Lake Store를 두 가지 방식으로 사용할 수 있습니다.

* Hello 기본 저장소로
* 추가 저장소로, Azure Storage Blob을 기본 저장소로.

현재, 일부 hello HDInsight 클러스터 데이터 레이크 저장소를 사용 하 여 기본 저장소 및 저장소 계정으로 형식/버전 지원:

| HDInsight 클러스터 유형 | 기본 저장소로 Data Lake Store | 추가 저장소로 Data Lake Store| 참고 |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight 버전 3.6 | 예 | 예 | |
| HDInsight 버전 3.5 | 예 | 예 | HBase의 hello 예외|
| HDInsight 버전 3.4 | 아니요 | 예 | |
| HDInsight 버전 3.3 | 아니요 | 아니요 | |
| HDInsight 버전 3.2 | 아니요 | 예 | |
| HDInsight 프리미엄(계층)| 아니요 | 아니요 | |
| Storm | | |데이터 레이크 저장소 toowrite 데이터 스톰 토폴로지를 사용할 수 있습니다. Storm 토폴로지에서 읽을 수 있는 참조 데이터에 Data Lake Store를 사용할 수도 있습니다.|

데이터 레이크 저장소를 사용 하 여 추가 저장소 계정으로 해도 성능 또는 기능 tooread hello에 영향을 또는 hello 클러스터에서 tooAzure 저장소 쓰기 되지 않습니다.


## <a name="use-data-lake-store-as-default-storage"></a>Data Lake Store를 기본 저장소로 사용

HDInsight 기본 저장소로 데이터 레이크 저장소에 배포 되 면 hello 클러스터 관련 파일 hello 수정할 수 있는 위치에에서 데이터 레이크 저장소에 저장 됩니다.

    adl://mydatalakestore/<cluster_root_path>/

여기서 `<cluster_root_path>` hello 데이터 레이크 저장소에 만들 폴더 이름입니다. 각 클러스터에 대 한 루트 경로 지정 하 여 사용할 수 있습니다 hello 둘 이상의 클러스터에 대 한 동일한 데이터 레이크 저장소 계정입니다. 따라서 다음 위치에 설정할 수 있습니다.

* Cluster1은 hello 경로 사용할 수 있습니다.`adl://mydatalakestore/cluster1storage`
* 클러스터 2 hello 경로 사용할 수 있습니다.`adl://mydatalakestore/cluster2storage`

클러스터 사용을 hello 모두 공지 hello 동일 데이터 레이크 저장소 계정 **mydatalakestore**합니다. 각 클러스터에 액세스 tooits 데이터 레이크 저장소에 루트 파일 시스템을 소유 합니다. Azure 포털 배포 환경을 hello 특히 묻는 toouse 폴더 이름을 같은 **/clusters/\<clustername >** hello 루트 경로 대 한 합니다.

toobe 수 toouse 기본 저장소로 데이터 레이크 저장소 경로 따라 hello 서비스 보안 주체 액세스 toohello를 부여 해야 합니다.

- hello 데이터 레이크 저장소 계정 루트입니다.  예: adl://mydatalakestore/.
- 클러스터의 모든 폴더에 대 한 hello 폴더입니다.  예: adl://mydatalakestore/clusters.
- hello 클러스터에 대 한 hello 폴더입니다.  예: adl://mydatalakestore/clusters/cluster1storage.

서비스 주체 및 액세스 부여에 대한 자세한 내용은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.


## <a name="use-data-lake-store-as-additional-storage"></a>추가 저장소로 Data Lake Store 사용

Hello 클러스터에 대 한 추가 저장소로 데이터 레이크 저장소를 사용할 수 있습니다. 이러한 경우 기본 저장소를 클러스터 하는 hello 데이터 레이크 저장소 계정 또는 Azure 저장소 Blob 일 수 있습니다. 추가 저장소로 데이터 레이크 저장소에 저장 된 hello 데이터에 대 한 HDInsight 작업을 실행 하는 경우에 hello 정식 경로 toohello 파일을 사용 해야 합니다. 예:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

없는 **cluster_root_path** hello URL 이제에 합니다. 데이터 레이크 저장소는 기본 저장소가 경우 아니므로 하기만 하면 toodo hello 경로 toohello 파일 제공 때문입니다.

toobe 수 toouse 추가 저장소로 데이터 레이크 저장소 하기만 하면 toogrant hello 서비스 보안 주체 액세스 toohello 경로 파일이 저장 되어 있습니다.  예:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

서비스 주체 및 액세스 부여에 대한 자세한 내용은 [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.


## <a name="use-more-than-one-data-lake-store-accounts"></a>둘 이상의 Data Lake Store 계정 사용

데이터 레이크 저장소 계정을 추가 하는 추가으로 및 둘 이상의 데이터 레이크 저장소 추가 계정은 데이터 내용을 한 번 이상 Data Lake 저장소 계정에 대해 hello HDInsight 클러스터 권한을 제공 하 여 수행 됩니다. [Data Lake Store 액세스 구성](#configure-data-lake-store-access)을 참조하세요.

## <a name="configure-data-lake-store-access"></a>Data Lake Store 액세스 구성

tooconfigure HDInsight 클러스터에서 데이터 레이크 저장소 액세스는 Azure Active directory (Azure AD) 서비스 사용자는 있어야 합니다. Azure AD 관리자만 서비스 주체를 만들 수 있습니다. 인증서로 hello 서비스 사용자를 만들어야 합니다. 자세한 내용은 [Data Lake Store 액세스 구성](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) 및 [자체 서명된 인증서로 서비스 주체 만들기](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate)를 참조하세요.

> [!NOTE]
> HDInsight 클러스터에 대 한 추가 저장소로 toouse Azure 데이터 레이크 저장소 하려는 경우 이렇게 하는 동안이 문서에 설명 된 대로 hello 클러스터를 만드는 것이 좋습니다. 추가 저장소 tooan로 Azure 데이터 레이크 저장소 추가 기존 HDInsight 클러스터는 복잡 한 프로세스 및 tooerrors 발생 하기 쉽습니다.
>

## <a name="access-files-from-hello-cluster"></a>Hello 클러스터에서 파일 액세스

여러 가지 방법으로 HDInsight 클러스터에서 데이터 레이크 저장소의 hello 파일에 액세스할 수 있습니다.

* **Hello 정규화 된 이름을 사용 하 여**합니다. 이 방법에서는 hello 전체 경로 toohello 파일을 제공 하 tooaccess 되도록 합니다.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Hello 축약된 경로 형식을 사용 하 여**합니다. 이 방법을 사용 하면 hello 경로 바꿉니다 toohello 클러스터 루트를 adl: / / /입니다. 따라서 위의 hello 예제에서 바꿀 수 있습니다 `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` 와 `adl:///`합니다.

        adl:///<file path>

* **Hello 상대 경로 사용 하 여**합니다. 이 방법을 사용 하면만 파일을 제공 hello 상대 경로 toohello tooaccess 되도록 합니다. 예를 들어 hello toohello 파일 전체 경로 경우 나요?

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    에 액세스할 수 있습니다이 상대 경로 대신 사용 하 여 동일한 sample.log 파일 hello 합니다.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>HDInsight 클러스터를 만들려면 액세스할 tooData Lake 저장소

HDInsight 클러스터를 toocreate tooData Lake 저장소를 액세스 하는 방법에 자세한 지침에 대 한 링크를 따라 hello를 사용 합니다.

* [포털 사용](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell 사용(Data Lake Store를 기본 저장소로)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [PowerShell 사용(Data Lake Store를 추가 저장소로)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Azure 템플릿 사용](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>다음 단계
이 문서에서는 방법에 대해 배웠습니다 toouse HDFS 호환 HDInsight와 Azure 데이터 레이크 저장소입니다. 이렇게 하면 구조화 되지 않은 데이터 및 데이터 취득 솔루션 및 구성 저장 hello 내부의 HDInsight toounlock hello 정보를 사용 하 여 보관 toobuild 확장 가능 하 고 장기, 있습니다.

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
