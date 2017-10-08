---
title: "데이터 레이크 저장소 MapReduce 성능 튜닝 지침 aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store MapReduce 성능 조정 지침"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a>HDInsight and Azure Data Lake Store에서 MapReduce에 대한 성능 조정 지침


## <a name="prerequisites"></a>필수 조건

* **Azure 구독**. [Azure 무료 평가판](https://azure.microsoft.com/pricing/free-trial/)을 참조하세요.
* **Azure 데이터 레이크 저장소 계정**. 방법에 대 한 지침은 toocreate 하나, 참조 [Azure 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* **Azure HDInsight 클러스터** 액세스 tooa 데이터 레이크 저장소 계정 사용 합니다. [Data Lake Store가 있는 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)를 참조하세요. Hello 클러스터에 대 한 원격 데스크톱을 사용 해야 합니다.
* **HDInsight에서 MapReduce 사용**.  자세한 내용은 [HDInsight에서 Hadoop과 MapReduce 사용](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)을 참조하세요.  
* **ADLS에서 성능 조정 지침**.  일반적인 성능 개념은 [Data Lake Store 성능 조정 지침](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)을 참조하세요.  

## <a name="parameters"></a>매개 변수

MapReduce 작업을 실행할 때 ADLS에서 tooincrease 성능을 구성할 수 있습니다 hello 가장 중요 한 매개 변수 다음과 같습니다.

* **Mapreduce.map.memory.mb** – hello 양의 메모리 tooallocate tooeach 매퍼
* **Mapreduce.job.maps** – hello 작업당 맵 작업 수
* **Mapreduce.reduce.memory.mb** – 메모리 tooallocate tooeach 리 듀 서의 hello 양
* **Mapreduce.job.reduces** – hello 작업당 reduce 작업 수

**Mapreduce.map.memory / Mapreduce.reduce.memory** 이 숫자 hello 지도에 얼마나 많은 메모리가 필요에 따라 조정 해야 및/또는 작업을 줄입니다.  hello 및 기본값을 mapreduce.map.memory mapreduce.reduce.memory hello Yarn 구성을 통해 Ambari에서 볼 수 있습니다.  Ambari를 tooYARN 이동한 hello Configs 탭을 표시 합니다.  hello YARN 메모리에 표시 됩니다.  

**Mapreduce.job.maps / Mapreduce.job.reduces** 이 만든 매퍼 또는 이경소켓 toobe hello 최대 수를 결정 합니다.  hello MapReduce 작업에 대 한 개수 매퍼 만들어집니다 hello 분할 수가 결정 됩니다.  따라서 요청 매퍼 hello 개수 보다 작은 분할이 많은 경우 요청 된 수보다 덜 매퍼 발생할 수 있습니다.       

## <a name="guidance"></a>지침

**1 단계: 실행 중인 작업의 수를 결정** -기본적으로 MapReduce에서 hello 전체 클러스터 작업에 사용 하면 됩니다.  사용 가능한 컨테이너 보다 적은 매퍼를 사용 하 여 작은 hello 클러스터를 사용할 수 있습니다.  이 문서에 hello 설명서 hello만 응용 프로그램 클러스터에서 실행 중인 응용 프로그램을 가정 합니다.      

**2 단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** – 맵에 대 한 hello 메모리의 크기를 hello 및 줄이기 작업은 특정 작업에 종속 됩니다.  Tooincrease 동시성을 원하는 경우 hello 메모리 크기를 줄일 수 있습니다.  hello 동시에 실행 중인 작업 수가 hello 컨테이너 수에 따라 달라 집니다.  Hello 맵 편집기 또는 리 듀 서 당 메모리 양을 줄여 자세한 컨테이너를 만들 수, 동시에 더 많은 매퍼 또는 이경소켓 toorun 있도록 합니다.  너무 많이 감소 hello 메모리 양을 메모리 부족 일부 프로세스 toorun을 발생할 수 있습니다.  작업을 실행 하는 경우 힙 오류가 발생할 경우 맵 편집기 또는 리 듀 서 당 hello 메모리를 늘려야 합니다.  더 많은 컨테이너를 추가하면 각 컨테이너당 오버헤드가 더 추가되며 이로 인해 성능이 저하될 수 있다는 것을 고려해야 합니다.  다른 대체에서는 tooget 메모리가 더 높은 양의 메모리를 갖고 있는 클러스터를 사용 하 여 hello 클러스터의 노드 수가 증가 합니다.  더 많은 메모리를 더 많은 컨테이너 toobe을 사용 하는 더 많은 동시성 의미를 사용 하 고 있습니다.  

**3 단계: 총 YARN 메모리 확인** -tootune mapreduce.job.maps/mapreduce.job.reduces hello 사용 하기 위해 사용할 수 있는 총 YARN 메모리 크기를 고려해 야 합니다.  이 정보는 Ambari에 제공됩니다.  TooYARN를 탐색 하 고 hello Configs 탭을 표시 합니다.  hello YARN 메모리가이 창에 표시 됩니다.  클러스터 tooget hello 총 YARN 메모리에 hello 노드 수를 사용 하 여 hello YARN 메모리를 곱하기 해야 합니다.

    Total YARN memory = nodes * YARN memory per node
빈 클러스터를 사용 하는 경우 메모리 클러스터에 대 한 총 YARN 메모리 hello를 수 있습니다.  컨테이너의 매퍼 또는 이경소켓 toohello 번호 hello 수를 줄여 tooonly 사용 하 여 클러스터의 메모리의 부분을 선택할 수 있습니다 다른 응용 프로그램 메모리를 사용 하는 경우 원하는 toouse 합니다.  

**4 단계: YARN 컨테이너의 개수를 계산** – YARN 컨테이너 hello 작업에 사용할 수 있는 동시성의 hello 양을 지정 합니다.  총 YARN 메모리를 가져와 mapreduce.map.memory로 나눕니다.  

    # of YARN containers = total YARN memory / mapreduce.map.memory

**5 단계: 설정 mapreduce.job.maps/mapreduce.job.reduces** mapreduce.job.maps/mapreduce.job.reduces tooat 설정 최소 hello 수가 사용 가능한 컨테이너입니다.  결과 실험해볼 수 더 나은 성능을 얻을 수 있는 경우 매퍼 및 이경소켓 toosee hello 수를 늘려 추가 합니다.  매퍼 수가 늘어나면 추가 오버헤드가 발생하므로 매퍼 수가 너무 많으면 성능이 저하될 수 있음에 유의해야 합니다.  

CPU 예약 및 CPU 격리는 기본적으로 해제 되어 있으므로 hello YARN 컨테이너 수가 메모리에 따라 달라 집니다.

## <a name="example-calculation"></a>계산 예

현재 클러스터 D14 8 개의 노드로 이루어진 있고 toorun I/O 집약적인 작업을 원하는 경우를 가정해 보십시오.  다음은 작업을 수행 해야 하는 hello 계산입니다.

**1 단계: 실행 중인 작업의 수를 결정** -이 예에서는 작업이 하나만 실행을 hello은 가정 합니다.  

**2단계: mapreduce.map.memory/mapreduce.reduce.memory 설정** – 이 예에서는 I/O 집약적인 작업을 실행 중이고 맵 태스크에 대해 3GB 메모리면 충분하다고 결정합니다.

    mapreduce.map.memory = 3GB
**3단계: 총 YARN 메모리 결정**

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
**4단계: YARN 컨테이너 수 결정**

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

**5단계: mapreduce.job.maps/mapreduce.job.reduces 설정**

    mapreduce.map.jobs = 256

## <a name="limitations"></a>제한 사항

**ADLS 제한**

다중 테넌트 서비스로 ADLS는 계정 수준 대역폭 제한을 설정합니다.  이러한 한도 도달 하면 toosee 작업 실패를 시작 합니다. 이것은 태스크 로그에서 제한 오류를 확인하여 파악할 수 있습니다.  작업에 대한 대역폭이 더 필요한 경우 문의하세요.   

toocheck 조절 됩니다 가져오는 경우, 클라이언트 쪽 hello에 대 한 로깅을 tooenable hello 디버그를 해야 합니다. 그 방법은 다음과 같습니다.

1. Put hello hello log4j에서에서 속성에에서 속성 Ambari 다음 > YARN > 구성 > yarn log4j 고급: log4j.logger.com.microsoft.azure.datalake.store=DEBUG

2. 모든 hello 노드/서비스 hello 구성 tootake 효과 대 한 다시 시작 합니다.

3. 사용자는 제한에 이르기, hello YARN 로그 파일의 hello HTTP 429 오류 코드를 표시 됩니다. hello YARN 로그 파일을 /tmp/&lt;사용자&gt;/yarn.log

## <a name="examples-toorun"></a>예제 tooRun

toodemonstrate는 MapReduce Azure 데이터 레이크 저장소에서 실행 하는 방법 다음은 몇 가지 샘플 코드 hello 다음 설정으로 클러스터에서 실행 된 합니다.

* 16 노드 D14v2
* HDI 3.6을 실행하는 Hadoop 클러스터

시작 지점에 대 한 몇 가지 예제 명령 toorun MapReduce Teragen, Terasort과 Teravalidate 다음과 같습니다.  리소스에 따라 이러한 명령을 조정할 수 있습니다.

**Teragen**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

**Terasort**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

**Teravalidate**

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
