---
title: "데이터 레이크 저장소 하이브 성능 튜닝 지침 aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store Hive 성능 조정 지침"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a>HDInsight의 Hive 및 Azure Data Lake Store에 대한 성능 조정 지침

hello 기본 설정은 통해 여러 다른 사용 사례 tooprovide 좋은 성능을 설정 않았습니다.  I/O 집약적인 쿼리 하이브 튜닝된 tooget ADLS 성능이 향상 될 수 있습니다.  

## <a name="prerequisites"></a>필수 조건

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다. [Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요. Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.
* **HDInsight에서 Hive 실행**.  [사용 하 여 HDInsight의 Hive] toolearn, HDInsight의 Hive 작업을 실행 하는 방법에 대 한 참조 (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)
* **ADLS에서 성능 조정 지침**.  일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.

## <a name="parameters"></a>매개 변수

ADLS 성능 향상된을 위해 가장 중요 한 설정을 tootune hello 다음과 같습니다.

* **hive.tez.container.size** – 각 작업에 의해 사용 되는 메모리 양을 hello

* **tez.grouping.min-size** – 각 매퍼의 최소 크기

* **tez.grouping.max-size** – 각 매퍼의 최대 크기

* **hive.exec.reducer.bytes.per.reducer** – 각 리듀서의 크기

**hive.tez.container.size** -hello 컨테이너 크기에 따라 결정 메모리의 크기를 각 작업에 대해 사용할 수 있습니다.  이 hello 하이브에 hello 동시성 제어에 대 한 주 입력 합니다.  

**tez.grouping.min 크기** –이 매개 변수는 hello tooset 각 맵 편집기의 최소 크기입니다.  Hello 수가 매퍼 Tez 선택 하는 hello이 매개이 변수 값 보다 작은 경우 Tez 여기서 설정한 hello 값을 사용 합니다.  

**tez.grouping.max 크기** – tooset hello 각 맵 편집기의 최대 크기 hello 매개 변수를 사용 합니다.  Hello 수가 매퍼 Tez 선택 하는 hello이 매개이 변수 값 보다 큰 경우 Tez 여기서 설정한 hello 값을 사용 합니다.  

**hive.exec.reducer.bytes.per.reducer** –이 매개 변수는 각 리 듀 서의 hello 크기를 설정 합니다.  기본적으로 각 리듀서는 256MB입니다.  

## <a name="guidance"></a>지침

**Hive.exec.reducer.bytes.per.reducer 설정** – hello 기본값 hello 데이터를 압축 된 경우 잘 작동 합니다.  압축 된 데이터에 대 한 hello 리 듀 서의 hello 크기를 줄여야 합니다.  

**Set hive.tez.container.size** – 각 노드에서 메모리는 yarn.nodemanager.resource.memory-mb에 의해 지정되고 기본적으로 HDI 클러스터에서 제대로 설정해야 합니다.  이 YARN에 hello 적합 한 메모리를 설정에 대 한 자세한 내용은 참조 [게시](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)합니다.

I/O가 많은 작업용 hello Tez 컨테이너 크기 감소 하 여 많은 병렬 처리에서 이점을 얻을 수 있습니다. Hello 사용자 동시성을 향상 시키는 컨테이너가 더 이상 제공 합니다.  하지만 일부 Hive 쿼리에는 상당한 양의 메모리가 필요합니다(예: MapJoin).  Hello 작업에 충분 한 메모리가 없는 경우에 메모리 부족 예외가 런타임 동안 발생 합니다.  메모리 부족 예외가 표시 되 면 hello 메모리를 증가 해야 합니다.   

hello 동시 실행 되는 작업 또는 수가 병렬 처리는 hello 총 YARN 메모리에 의해 제한 됩니다.  동시 작업 수를 실행할 수 hello YARN 컨테이너 수가 결정 됩니다.  노드당 hello YARN 메모리 toofind tooAmbari 이동할 수 있습니다.  TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
ADLS를 사용 하 여 hello 키 tooimproving 성능을 최대한 많은 tooincrease hello 동시성입니다.  Tez hello 되므로 tooset 하지 않고도 만들어야 하는 작업 수를 자동으로 계산 것입니다.   

## <a name="example-calculation"></a>계산 예

8 노드 D14 클러스터가 있다고 가정해 보겠습니다.  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a>제한 사항
**ADLS 제한** 

Hello 적중 UIf toosee 작업 실패를 시작, ADLS 하 여 제공 된 대역폭의 제한 합니다. 이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.  Tez 컨테이너 크기를 늘려 hello 병렬 처리를 줄일 수 있습니다.  작업에 대한 동시성이 더 필요한 경우 문의하세요.   

toocheck 조절 됩니다 가져오는 경우, 클라이언트 쪽 hello에 대 한 로깅을 tooenable hello 디버그를 해야 합니다. 그 방법은 다음과 같습니다.

1. 하이브 config에서 hello log4j 속성에 속성을 다음 hello를 넣습니다. Ambari 보기에서이 작업을 수행할 수 있습니다: log4j.logger.com.microsoft.azure.datalake.store=DEBUG 모든 hello 노드/서비스를 다시 시작 hello 구성 tootake 효과입니다.

2. 스로틀 가져오기는, hello 하이브 로그 파일의 hello HTTP 429 오류 코드를 표시 됩니다. hello 하이브 로그 파일을 /tmp/&lt;사용자&gt;/hive.log

## <a name="further-information-on-hive-tuning"></a>Hive 조정에 대한 추가 정보

Hive 쿼리를 조정하는 데 도움이 되는 몇 가지 블로그는 다음과 같습니다.
* [HDInsight에서 Hadoop에 대한 Hive 쿼리 최적화](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [Hive 쿼리 성능 문제 해결](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [HDInsight에서 Hive 최적화에 대한 논의](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
