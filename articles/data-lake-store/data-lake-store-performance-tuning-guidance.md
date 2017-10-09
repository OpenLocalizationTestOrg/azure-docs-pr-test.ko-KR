---
title: "데이터 레이크 저장소 성능 튜닝 지침 aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store 성능 조정 지침"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Azure Data Lake Store의 성능 조정

Data Lake Store는 I/O 집약적 분석 및 데이터 이동에 대해 높은 처리량을 지원합니다.  Azure 데이터 레이크 저장소 사용 가능한 모든 처리량 – 읽거나 초당 쓰기 수 있는 데이터의 양을 hello-를 사용 하 여는 중요 한 tooget hello 최상의 성능입니다.  이를 위해 최대한 많은 읽기와 쓰기를 병렬로 수행합니다.

![Data Lake Store 성능](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure 데이터 레이크 저장소 tooprovide hello 모든 분석 시나리오에 대 한 필요한 처리량을 확장할 수 있습니다. 기본적으로 Azure 데이터 레이크 저장소 계정 사용 사례는 광범위 한 범주 toomeet hello 요구 자동으로 충분 한 처리량을 제공합니다. ADLS 계정 hello hello 경우 고객 hello 기본 한도를 실행 하는 위치에 대 한 Microsoft 지원에 문의 하 여 구성 된 tooprovide 처리량을 높일 수 있습니다.

## <a name="data-ingestion"></a>데이터 수집

원본 시스템 tooADLS에서 데이터를 수집 하는 방법, 경우에 중요 한 원본 하드웨어, 원본 네트워크 하드웨어 및 네트워크 연결 tooADLS hello tooconsider hello 병목 지점이 될 수 있습니다.  

![Data Lake Store 성능](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

데이터 이동 hello tooensure 이러한 요인에 의해 영향을 받지 않습니다 유용 합니다.

### <a name="source-hardware"></a>원본 하드웨어

사용 하 여 온-프레미스 컴퓨터 또는 Vm에 Azure를 hello 적절 한 하드웨어를 신중 하 게 선택 해야 합니다. 원본 디스크 하드웨어에 대 한 Ssd tooHDDs 선호 하 고 스핀 들이 더 빠른 디스크 하드웨어를 선택 하십시오. 원본 네트워크 하드웨어에 대 한 가장 빠른 Nic 가능한 hello를 사용 합니다.  Azure에서 Azure D14 Vm hello 적절 하 게 강력한 디스크 및 네트워킹 하드웨어를 포함 하는 것이 좋습니다.

### <a name="network-connectivity-tooazure-data-lake-store"></a>네트워크 연결 tooAzure 데이터 레이크 저장소

원본 데이터와 Azure 데이터 레이크 저장소 간의 네트워크 연결 hello hello 병목 수 있습니다. 원본 데이터가 온-프레미스인 경우 [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/)와 함께 전용 링크를 사용하는 것이 좋습니다. 원본 데이터를 Azure에 있으면, hello 성능이 되 최상의 hello에 hello 데이터가 있으면 hello 데이터 레이크 저장소와 같은 Azure 지역입니다.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>최대 병렬 처리를 위해 데이터 수집 도구 구성

Hello 소스 하드웨어 처리 하 고 네트워크 연결 병목 현상을 위의 준비 tooconfigure 됩니다 수집 도구입니다. hello 다음 표에 요약 여러 인기 있는 수집 도구에 대 한 hello 키 설정 하 고 제공 심층 분석 문서를 위한 성능 튜닝에 합니다.  이 toolearn toouse 시나리오에 대 한 도구에 대 한 내용은 방문 [문서](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios)합니다.

| 도구               | 설정     | 자세한 정보                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [링크](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Azure Data Lake Analytics 단위  |   [링크](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m(mapper)   | [링크](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure 데이터 팩터리| parallelCopies    | [링크](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | fs.azure.block.size, -m(mapper)    |   [링크](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>데이터 집합 구성

데이터 레이크 저장소 hello 파일 크기에에서 데이터가 저장 되 면 파일 및 폴더 구조 수 성능에 영향을 줄 합니다.  hello 다음 섹션에서는 이러한 영역 모범 사례  

### <a name="file-size"></a>파일 크기

일반적으로 HDInsight, Azure Data Lake Analytics 등의 분석 엔진에서는 파일당 오버헤드가 발생합니다.  데이터를 많은 작은 파일로 저장하는 경우 성능이 저하될 수 있습니다.  

일반적으로 성능을 향상하려면 데이터를 더 큰 파일로 구성합니다.  경험상, 데이터 집합을 256MB 이상의 파일로 구성합니다. 이미지 및 이진 데이터와 같은 일부 경우에 없는 가능한 tooprocess 동시에 해당 합니다.  이러한 경우 tookeep 개별 파일 2GB 미만 좋습니다.

경우에 따라 데이터 파이프라인에 다 수의 작은 파일 hello 원시 데이터에 대 한 제어를 제한 됩니다.  Toohave 좋습니다 큰를 생성 하는 "요리" 프로세스 toouse 다운스트림 응용 프로그램에 대 한 파일입니다.  

### <a name="organizing-time-series-data-in-folders"></a>시계열 데이터를 폴더로 구성

Hive 및 ADLA 작업에 대 한 시계열 데이터의 파티션 정리 일부 쿼리 성능을 향상 시키는 hello 데이터의 하위 집합만 읽을 수 있습니다.    

시계열 데이터를 수집하는 이러한 파이프라인은 파일 및 폴더에 대해 구조적 명명을 사용하여 파일을 배치하는 경우가 많습니다. 다음은 날짜별로 구성된 데이터에서 매우 일반적으로 나타나는 예입니다.

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

Datetime 정보 hello 폴더 및 파일 이름 hello에에서 나타나는지 확인 합니다.

날짜 및 시간에 대 한 hello 다음은 일반 패턴

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

마찬가지로 한 hello 더 큰 파일 크기 및 각 폴더에 있는 파일의 수를 적절 한 hello 선택 hello 폴더 및 파일 조직과 최적화 해야 합니다.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>HDInsight의 Hadoop 및 Spark 워크로드에 대한 I/O 집약적 작업 최적화

작업은 hello 다음 세 가지 범주 중 하나에 속합니다.

* **CPU 집약적.**  이러한 작업은 최소한의 I/O 시간으로 계산 시간이 깁니다.  기계 학습 및 자연어 처리 작업을 예로 들 수 있습니다.  
* **메모리 집약적.**  이러한 작업은 메모리를 많이 사용합니다.  PageRank 및 실시간 분석 작업을 예로 들 수 있습니다.  
* **I/O 집약적.**  이러한 작업은 I/O를 수행하는 데 대부분의 시간을 사용합니다.  읽기 및 쓰기 작업만 수행하는 복사 작업이 일반적인 예입니다.  다른 예로 많은 데이터 읽기, 일부 데이터 변환을 수행 하는 데이터 준비 작업 하 고 쓰기 hello 데이터 백 toohello 저장소 키를 누릅니다.  

hello 지침은 적용 가능한 tooI/O 집약적 작업입니다.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>HDInsight 클러스터에 대한 일반적인 고려 사항

* **HDInsight 버전.** 최상의 성능을 위해 HDInsight의 최신 릴리스에 hello를 사용 합니다.
* **지역.** 데이터 레이크 저장소 hello hello에 배치 hello HDInsight 클러스터와 동일한 지역입니다.  

HDInsight 클러스터는 헤드 노드 두 개와 일부 작업자 노드로 구성됩니다. 각 작업자 노드는 특정 코어 수와 hello VM 유형에 의해 결정 되는 메모리를 제공 합니다.  작업을 실행할 때 YARN hello 사용 가능한 메모리 및 코어 toocreate 컨테이너에서 할당 하는 hello 리소스 협상 자입니다.  각 컨테이너는 hello 작업 필요한 toocomplete hello 작업을 실행합니다.  컨테이너는 신속 하 게 병렬 tooprocess 작업에서 실행 됩니다. 따라서 최대한 많은 병렬 컨테이너를 실행하여 성능을 향상합니다.

튜닝 된 tooincrease 일 수 있는 HDInsight 클러스터 내에서 3 계층 hello 컨테이너의 개수 및 사용 가능한 모든 처리량을 사용 합니다.  

* **물리적 계층**
* **YARN 계층**
* **워크로드 계층**

### <a name="physical-layer"></a>물리적 계층

**더 많은 노드 및/또는 더 큰 VM으로 클러스터를 실행합니다.**  대규모 클러스터를 사용 하면 toorun 아래 hello 그림에 표시 된 대로 YARN 컨테이너가 더 이상 있습니다.

![Data Lake Store 성능](./media/data-lake-store-performance-tuning-guidance/VM.png)

**더 많은 네트워크 대역폭을 가진 VM을 사용합니다.**  데이터 레이크 저장소 처리량 보다 네트워크 대역폭을 덜는 네트워크 대역폭 양을 hello 병목 상태가 될 수 있습니다.  VM마다 각기 다른 네트워크 대역폭 크기를 갖게 됩니다.  가장 큰 가능한 네트워크 대역폭이 hello VM 유형을 선택 하십시오.

### <a name="yarn-layer"></a>YARN 계층

**더 작은 YARN 컨테이너를 사용합니다.**  Hello로 컨테이너가 더 이상 각 YARN 컨테이너 toocreate의 hello 크기를 줄이려면 같은 양의 리소스입니다.

![Data Lake Store 성능](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

워크로드에 따라 항상 필요한 최소 YARN 컨테이너 크기가 있습니다. 너무 작은 컨테이너를 선택하면 작업에서 메모리 부족 문제가 발생합니다. 일반적으로 YARN 컨테이너는 1GB 이상이어야 합니다. 일반적인 toosee 3GB YARN 컨테이너 이며 일부 워크로드의 경우 더 큰 YARN 컨테이너가 필요할 수도 있습니다.  

**YARN 컨테이너당 코어 수를 늘립니다.**  Hello tooeach 컨테이너 tooincrease hello 개수의 병렬 작업이 각 컨테이너를 실행 하는 할당 된 코어 수를 증가 합니다.  이 방법은 컨테이너당 여러 태스크를 실행하는 Spark 등의 응용 프로그램에 적합합니다.  응용 프로그램 Hive와 같은 각 컨테이너에는 단일 스레드 실행 하는 컨테이너 당 더 많은 코어를 사용 하지 않고 컨테이너가 더 이상 toohave 정보가 개선 되었습니다.   

### <a name="workload-layer"></a>워크로드 계층

**사용 가능한 모든 컨테이너를 이용합니다.**  모든 리소스 사용 되는지에 있도록 사용 가능한 컨테이너에서 hello 수보다 크거나 hello 수가 작업 toobe 설정 합니다.

![Data Lake Store 성능](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**실패한 태스크는 비용이 많이 듭니다.** 각 작업에 많은 양의 데이터 tooprocess 작업의 실패는 비용이 많이 드는 다시 시도에서 발생 합니다.  따라서 것이 더 나은 toocreate 더 많은 작업을 각각 적은 양의 데이터를 처리 합니다.

또한 toohello 일반 위의 지침, 각 응용 프로그램에는 해당 특정 응용 프로그램에 대 한 다양 한 매개 변수의 사용 가능한 tootune 있습니다. hello 아래 표에 일부 hello 매개 변수 및 링크 tooget 각 응용 프로그램에 대 한 성능 튜닝을 시작 합니다.

| 워크로드               | 매개 변수 tooset 작업                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [HDInisight의 Spark](data-lake-store-performance-tuning-spark.md)       | <ul><li>Num-executors</li><li>Executor-memory</li><li>Executor-cores</li></ul> |
| [HDInsight의 Hive](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.size</li></ul>         |
| [HDInsight의 MapReduce](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>Mapreduce.map.memory</li><li>Mapreduce.job.maps</li><li>Mapreduce.reduce.memory</li><li>Mapreduce.job.reduces</li></ul> |
| [HDInsight의 Storm](data-lake-store-performance-tuning-storm.md)| <ul><li>작업자 프로세스 수</li><li>Spout 실행자 인스턴스 수</li><li>Bolt 실행자 인스턴스 수 </li><li>Spout 작업 수</li><li>Bolt 작업 수</li></ul>|

## <a name="see-also"></a>참고 항목
* [Azure 데이터 레이크 저장소 개요](data-lake-store-overview.md)
* [Azure 데이터 레이크 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
