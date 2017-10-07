---
title: "Distcp를 사용 하 여 데이터 레이크 저장소로 WASB에서 aaaCopy 데이터 tooand | Microsoft Docs"
description: "Azure 저장소 Blob tooData 레이크 스토어에서 Distcp 도구 toocopy 데이터 tooand 사용"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a>Azure 저장소 Blob 및 azure 데이터 레이크 저장소 간에 Distcp toocopy 데이터를 사용 하 여
> [!div class="op_single_selector"]
> * [DistCp 사용](data-lake-store-copy-data-wasb-distcp.md)
> * [AdlCopy 사용](data-lake-store-copy-data-azure-storage-blob.md)
>
>

에 대 한 액세스 tooa 데이터 레이크 저장소 계정이 HDInsight 클러스터를 만든 후 Distcp toocopy 데이터와 같은 Hadoop 에코 시스템 도구를 사용할 수 있습니다 **에서 tooand** 데이터 레이크 저장소 계정에 HDInsight 클러스터 저장소 (WASB). 이 문서는 방법에 대해 설명 tooachieve이 있습니다.

## <a name="prerequisites"></a>필수 조건
이 문서를 시작 하기 전에 hello 다음이 있어야 합니다.

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다. [Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요. Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.

## <a name="do-you-learn-fast-with-videos"></a>비디오로 빠르게 배우시겠습니까?
[이 비디오를 시청](https://mix.office.com/watch/1liuojvdx6sie) 방법에 Azure 저장소 Blob와 DistCp를 사용 하 여 데이터 레이크 저장소 간에 toocopy 데이터입니다.

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a>HDInsight Linux 클러스터에서 Distcp 사용

HDInsight 클러스터는 HDInsight 클러스터에 서로 다른 원본에서 사용 되는 toocopy 데이터 될 수 있는 hello Distcp 유틸리티와 함께 제공 됩니다. 추가 저장소로 hello HDInsight 클러스터 toouse Data Lake 저장소를 구성한 경우 hello Distcp 유틸리티 수 있습니다. 사용 된 데이터 레이크 저장소 계정에서 기본적으로 toocopy 데이터 tooand. 이 섹션에서는 toouse Distcp 유틸리티 hello 하는 방법을 살펴보겠습니다.

1. 바탕 화면에서 SSH tooconnect toohello 클러스터를 사용 합니다. 참조 [연결 tooa Linux 기반 HDInsight 클러스터](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md)합니다. Hello SSH 프롬프트에서 hello 명령을 실행 합니다.

2. Azure 저장소 Blob (WASB) hello에 액세스할 수 있는지 확인 합니다. Hello 다음 명령을 실행 합니다.

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    이 hello 저장소 blob의 콘텐츠 목록을 제공 해야 합니다.
3. 마찬가지로, hello 클러스터에서 hello 데이터 레이크 저장소 계정에 액세스할 수 있는지 확인 합니다. Hello 다음 명령을 실행 합니다.

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    이 hello Data Lake 저장소 계정에서에서 파일/폴더의 목록을 제공 해야 합니다.
4. WASB tooa Data Lake 저장소 계정에서에서 Distcp toocopy 데이터를 사용 합니다.

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    이렇게 하면 hello의 hello 내용을 복사 됩니다 **/예제/데이터/gutenberg/** WASB에서 폴더 너무**/myfolder** hello Data Lake 저장소 계정에서에서 합니다.
5. 마찬가지로, Data Lake 저장소 계정 tooWASB에서 Distcp toocopy 데이터를 사용 합니다.

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    hello 내용을 복사 됩니다 **/myfolder** hello 데이터 레이크 저장소에서에서 계정을 너무**/예제/데이터/gutenberg/** WASB에서 폴더입니다.

## <a name="performance-considerations-while-using-distcp"></a>DistCp 사용에 대한 성능 고려 사항

세분성은 단일 파일, 동시 복사본의 설정 hello 최대 수는 가장 중요 한 매개 변수 toooptimize hello DistCp의 가장 낮은 때문에 데이터 레이크 저장소에 대 한 것입니다. 이 매퍼 hello 수를 설정 하 여 제어 됩니다 (am') hello 명령줄에서 매개 변수입니다. 이 매개 변수는 hello 매퍼 사용된 toocopy 데이터 수 있는 최대 수를 지정 합니다. 기본값은 20입니다.

**예제**

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a>매퍼 toouse hello 수를 확인 하려면 어떻게 해야 합니까?

다음은 사용할 수 있는 몇 가지 지침입니다.

* **1 단계: 총 YARN 메모리를 확인할** -hello 첫 번째 단계는 toodetermine hello YARN 메모리 사용 가능한 toohello 클러스터 hello DistCp 작업을 실행 하는 위치입니다. 이 정보는 hello 클러스터와 연결 된 hello Ambari 포털에서 사용할 수 있습니다. TooYARN 찾아 hello Configs 탭 toosee hello YARN 메모리를 봅니다. tooget hello 총 YARN 메모리 hello YARN 노드별로 메모리를 hello 노드 수와 클러스터에 있는 여러 번입니다.

* **2 단계: 매퍼 hello 수를 계산** -의 값을 hello **m** YARN 컨테이너 크기 hello로 나눈 총 YARN 메모리의 같은 toohello quotient는 합니다. hello YARN 컨테이너 크기 정보 hello Ambari 포털 에서도 제공 됩니다. TooYARN 이동한 보기 hello Configs 탭 hello YARN 컨테이너 크기가이 창에 표시 됩니다. hello 수 매퍼의 수식 tooarrive hello (**m**)은

        m = (number of nodes * YARN memory for each node) / YARN container size

**예제**

Hello 클러스터에 4 D14v2s 노드가 있는 고 tootransfer 10TB 고치려는 가정 10 서로 다른 폴더에서 데이터입니다. 다양 한 양의 데이터를 포함 하는 각 hello 폴더 되며 각 폴더 내의 hello 파일 크기가 서로 다릅니다.

* 전체 YARN-hello 해당 hello YARN 메모리 확인은 Ambari 포털에서에서 메모리가 96GB D14 노드에 대 한 합니다. 따라서 4노드 클러스터의 전체 YARN 메모리는 다음과 같습니다. 

        YARN memory = 4 * 96GB = 384GB

* Hello 해당 hello YARN 컨테이너 크기는 3072 D14 클러스터 노드에 대 한 확인은 Ambari 포털에서에서 매퍼-수입니다. 따라서 매퍼 수는 다음과 같습니다.

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

다른 응용 프로그램 메모리를 사용 하는 경우 다음 선택할 수 있습니다 tooonly 사용 하 여 클러스터의 YARN 메모리의 일부 DistCp에 대 한.

### <a name="copying-large-datasets"></a>큰 데이터 집합 복사

매우 크면 hello dataset toobe의 hello 크기 이동한 경우 (예: > 1TB) 또는 여러 폴더를 사용 하도록 설정한 경우 여러 DistCp 작업을 사용 하 여 고려해 야 합니다. 가능성이 성능이 향상 되지 않습니다 있지만 모든 작업이 실패 한 경우 하기만 하면 됩니다 toorestart 해당 특정 작업 보다는 전체 작업 hello 있도록 hello 업무 분산 됩니다.

### <a name="limitations"></a>제한 사항

* DistCp 크기 toooptimize 성능이 유사한 toocreate 매퍼를 시도 합니다. 매퍼의 hello 수를 늘리면 성능 항상 늘리지 않을 수 있습니다.

* DistCp 제한 tooonly 파일당 한 매퍼입니다. 따라서 파일 개수보다 매퍼가 더 많지 않아야 합니다. DistCp만 할당할 수 하나의 매퍼 tooa 파일을이 hello 동시 처리량을 사용 하는 toocopy 큰 파일 수를 제한 합니다.

* 적은 수의 큰 파일을 있는 경우 256MB 파일 청크 toogive로 분할 해야 하면 더 많은 잠재적 동시성 합니다. 
 
* Azure Blob 저장소 계정에서 복사 하는 경우 복사 작업 hello blob 저장소 쪽 제한 될 수 있습니다. 이 복사 작업의 hello 성능이 저하 됩니다. Azure Blob 저장소의 hello 제한에 대 한 더 toolearn 참조에서 Azure 저장소 제한 [Azure 구독 및 서비스 제한](../azure-subscription-service-limits.md)합니다.

## <a name="see-also"></a>참고 항목
* [Azure 저장소 Blob tooData Lake 저장소에서 데이터 복사](data-lake-store-copy-data-azure-storage-blob.md)
* [데이터 레이크 저장소의 데이터 보호](data-lake-store-secure-data.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Azure HDInsight에 데이터 레이크 저장소 사용](data-lake-store-hdinsight-hadoop-use-portal.md)
