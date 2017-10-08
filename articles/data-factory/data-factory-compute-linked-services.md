---
title: "Azure Data Factory에서 지 원하는 aaaCompute 환경 | Microsoft Docs"
description: "Azure 데이터 팩터리 파이프라인 (예: Azure HDInsight) tootransform 또는 프로세스 데이터에서 사용할 수 있는 컴퓨팅 환경에 대해 알아봅니다."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 6877a7e8-1a58-4cfb-bbd3-252ac72e4145
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 07/25/2017
ms.author: shlo
ms.openlocfilehash: aba7d7de695bc1c7d475f1e741ee3b3e884151c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Azure Data Factory에서 지원하는 컴퓨팅 환경
이 문서에서는 다른 계산 환경 tooprocess를 사용 하 여 또는 데이터를 변형할 수 있습니다. 또한 이러한 계산 환경 tooan Azure 데이터 팩터리에 연결 하는 연결 된 서비스를 구성할 때 Data Factory에서 지 원하는 다른 구성 (주문형 스트림과 bring 직접)에 대 한 세부 정보를 제공 합니다.

hello 다음 표에서 계산 환경에서 실행할 수 있는 Data Factory와 hello 활동에서 지 원하는 목록을. 

| 컴퓨팅 환경 | 작업 |
| --- | --- |
| [주문형 HDInsight 클러스터](#azure-hdinsight-on-demand-linked-service) 또는 [사용자 고유의 HDInsight 클러스터](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md) |
| [Azure 배치](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure 기계 학습](#azure-machine-learning-linked-service) |[Machine Learning 작업: 배치 실행 및 업데이트 리소스](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure 데이터 레이크 분석](#azure-data-lake-analytics-linked-service) |[데이터 레이크 분석 U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[저장 프로시저](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Azure Data Factory에서 지원되는 HDInsight 버전
Azure HDInsight는 언제든 배포할 수 있는 여러 Hadoop 클러스터 버전을 지원합니다. 각 버전 선택 사항을 hello Hortonworks Data Platform (HDP) 배포의 특정 버전 및 해당 배포에 포함 된 구성 요소 집합을 만듭니다. HDInsight tooprovide 최신 Hadoop 에코 시스템 구성 요소 및 수정 프로그램의 지원 되는 버전의 hello 목록을 업데이트 하는 Microsoft 유지 합니다. hello HDInsight 3.2 2017 년 4 월 1에서 사용 되지 않습니다. 자세한 내용은 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.

이로 인해 HDInsight 3.2 클러스터에 대해 실행되는 활동이 있는 기존 Azure Data Factory에 영향을 미칩니다. 사용자가 toofollow hello 지침 섹션 tooupdate 다음 hello에 영향을 받는 데이터 팩터리 hello 하는 것이 좋습니다.

### <a name="for-linked-services-pointing-tooyour-own-hdinsight-clusters"></a>연결 된 서비스에 대 한 tooyour 자체 HDInsight 클러스터를 가리키는
* **3.2 또는 클러스터 아래 HDInsight를 소유 하는 HDInsight 연결 된 서비스를 가리키는 tooyour:**

  Azure Data Factory 지원 자체 HDInsight 클러스터 HDI 3.1에서 너무 제출 작업 tooyour[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다. 그러나 더 이상 후 만들 수 없습니다 3.2 HDInsight 클러스터에서 설명 하는 hello 사용 중단 정책에 따라 2017 년 4 월 1 [지원 되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다.  

  **권장 사항:** 
  * 테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 에 설명 된 정보로 [Hadoop 사용할 수 있는 구성 요소 다른 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.
  * 3.2 HDInsight 클러스터를 너무 업그레이드[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 수정 합니다. 

* **3.3 또는 클러스터 위에 HDInsight를 소유 하는 HDInsight 연결 된 서비스를 가리키는 tooyour:**

  Azure Data Factory 지원 자체 HDInsight 클러스터 HDI 3.1에서 너무 제출 작업 tooyour[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)합니다. 
  
  **권장 사항:** 
  * Data Factory 관점에서 보면 아무런 작업도 필요하지 않습니다. 그러나 HDInsight의 낮은 버전에 있는 경우 여전히 줄이려면 업그레이드 너무[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 수정 합니다.

### <a name="for-hdinsight-on-demand-linked-services"></a>주문형 HDInsight 연결된 서비스의 경우
* **주문형 HDInsight 연결된 서비스 JSON 정의에 지정되어 있는 버전 3.2 이하:**
  
  Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다. 와 연결 된 서비스 너무 확장은 기존 주문형 HDInsight 3.2에 대 한 지원의 hello 끝**2017/15/07**합니다.  

  **권장 사항:** 
  * 테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행 [최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 에 설명 된 정보로 [Hadoop 사용할 수 있는 구성 요소 다른 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.
  * 하기 전에 **2017/15/07**, 주문형 HDI 연결 된 서비스 JSON 정의에서 hello Version 속성을 너무 업데이트[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) tooget hello 최신 Hadoop 에코 시스템 구성 요소 및 해결합니다. 자세한 JSON 정의 대 한 참조 toohello [Azure HDInsight 주문형 연결 된 서비스 샘플](#azure-hdinsight-on-demand-linked-service)합니다. 

* **주문형 HDInsight 연결된 서비스에 지정되지 않은 버전:**
  
  Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다. 지원 tooexisting 주문형 HDInsight 3.2 연결 된 서비스의 hello 끝 너무 확장 되 고**2017/15/07**합니다. 

  하기 전에 **2017/15/07**, hello 기본 버전에 대 한 값을 입력 하지 않으면 및 osType 속성입니다. 

  | 속성 | 기본값 | 필수 |
  | --- | --- | --- |
  버전   | Windows 클러스터용 HDI 3.1 및 Linux 클러스터용 HDI 3.2| 아니요
  osType | hello 기본값은 Windows | 아니요

  후 **2017/15/07**, hello 기본 버전에 대 한 값을 입력 하지 않으면 및 osType 속성입니다.

  | 속성 | 기본값 | 필수 |
  | --- | --- | --- |
  버전   | Windows 클러스터용 HDI 3.3 및 Linux 클러스터용 3.5.    | 아니요
  osType | hello 기본값은 Linux   | 아니요

  **권장 사항:** 
  * 하기 전에 **2017/15/07**, 테스트 tooensure hello 호환성 hello 너무이 연결 된 서비스를 참조 하는 작업의 수행[최신 지원 hello HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions) 설명 정보로 [Hadoop 다른 HDInsight 버전을 사용할 수 있는 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [Hortonworks 릴리스 정보 HDInsight 버전에 연결 된](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)합니다.  
  * 후 **2017/15/07**, toooverride hello 기본 설정을 선택 하는 경우 osType 및 버전 값을 명시적으로 지정 했는지 확인 하십시오. 

>[!Note]
>현재 Azure Data Factory는 Azure Data Lake Store를 기본 저장소로 사용하는 HDInsight 클러스터를 지원하지 않습니다. Azure Storage를 HDInsight 클러스터의 기본 저장소로 사용합니다. 
>  
>  

## <a name="on-demand-compute-environment"></a>주문형 계산 환경
이러한 유형의 구성 hello 컴퓨팅 환경은 완전히 hello Azure 데이터 팩터리 서비스에서 관리 됩니다. 자동으로 작업은 전송 된 tooprocess 데이터 전에 hello 데이터 팩터리 서비스에서 만든 및 hello 작업이 완료 될 때 제거 됩니다. Hello 요청 시 계산 환경에 대 한 연결 된 서비스를 만들 지정, 구성, 및 작업 실행, 클러스터 관리 및 작업 부트스트랩에 대 한 세부적인 설정을 제어 합니다.

> [!NOTE]
> 요청 시 구성 hello는 현재 Azure HDInsight 클러스터에만 지원 됩니다.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight 주문형 연결된 서비스
hello Azure 데이터 팩터리 서비스는 Windows/Linux 기반에 주문형 HDInsight 클러스터 tooprocess 데이터를 자동으로 만들 수 있습니다. hello 클러스터 hello hello 클러스터와 연결 된 hello 저장소 계정 (hello JSON의에서 linkedServiceName 속성)와 동일한 지역에에서 생성 됩니다. hello 저장소 계정에는 범용 표준 Azure 저장소 계정 이어야 합니다. 

Hello 다음에 유의 하십시오 **중요** 포인트에 대 한 주문형 HDInsight 연결 된 서비스:

* 요청 시 hello 표시 되지 않으면 Azure 구독에서 생성 하는 HDInsight 클러스터입니다. hello Azure 데이터 팩터리 서비스에서 사용자 대신 hello 주문형 HDInsight 클러스터를 관리합니다.
* hello 주문형 HDInsight 클러스터에서 실행 되는 작업에 대 한 로그 복사 hello HDInsight 클러스터와 연결 된 toohello 저장소 계정. Hello hello에서 Azure 포털에서에서 이러한 로그에 액세스할 수 **작업 실행 세부 정보** 블레이드입니다. 세부 정보는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하십시오.
* Hello HDInsight 클러스터를 가장 하는 hello 시간 및 실행 되는 작업에 대해서만 청구 됩니다.

> [!IMPORTANT]
> 일반적으로 걸리는 **20 분** 또는 필요에 따라 더 많은 tooprovision Azure HDInsight 클러스터입니다.
> 
> 

### <a name="example"></a>예제
다음 JSON hello Linux 기반에 주문형 HDInsight 연결 된 서비스를 정의 합니다. hello 데이터 팩터리 서비스를 자동으로 만듭니다는 **Linux 기반** HDInsight 클러스터는 데이터 조각을 처리 하는 경우. 

```json
{
    "name": "HDInsightOnDemandLinkedService",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "version": "3.5",
            "clusterSize": 1,
            "timeToLive": "00:05:00",
            "osType": "Linux",
            "linkedServiceName": "AzureStorageLinkedService"
        }
    }
}
```

Windows 기반 HDInsight 클러스터 toouse 설정 **osType** 너무**windows** hello 기본값 그대로 hello 속성을 사용 하지 않는 또는: windows 합니다.  

> [!IMPORTANT]
> hello HDInsight 클러스터를 만듭니다는 **기본 컨테이너** hello JSON에에서 지정 된 hello blob 저장소에 (**linkedServiceName**). HDInsight 클러스터 hello 삭제 될 때이 컨테이너를 삭제 하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결 된 서비스와 HDInsight 클러스터를 분할 영역 해야 처리 하지 않으면 기존 라이브 클러스터 toobe 때마다 만드는 (**timeToLive**) hello 처리가 완료 되 면 삭제 됩니다. 
> 
> 많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. Toodelete 경우가 해당 hello 작업의 문제 해결을 위해 필요 하지 않은 경우 해당 tooreduce hello 저장소 비용을 합니다. 이러한 컨테이너의 hello 이름 패턴을 따르도록: `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp`합니다. 와 같은 도구를 사용 하 여 [Microsoft 저장소 탐색기](http://storageexplorer.com/) toodelete 컨테이너에 Azure blob 저장소입니다.
> 
> 

### <a name="properties"></a>properties
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**HDInsightOnDemand**합니다. |예 |
| clusterSize |Hello 클러스터의 작업자/데이터 노드 수입니다. hello HDInsight 클러스터는 헤드 노드 hello이이 속성에 대해 지정 하는 작업자 노드 수와 함께 2으로 생성 됩니다. hello 노드는 크기는 4 작업자 노드 클러스터는 24 코어 4 개 코어에 Standard_D3 (4\*작업자 노드 + 2에 대 한 4 = 16 코어가\*헤드 노드에 대 한 4 = 8 코어). 참조 [HDInsight 클러스터를 만드는 Linux 기반 Hadoop](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md) hello Standard_D3 계층에 대 한 세부 정보에 대 한 합니다. |예 |
| timetolive |hello는 hello 주문형 HDInsight 클러스터에 대 한 유휴 시간을 허용 합니다. 기간 hello 주문형 HDInsight 클러스터의 연결이 유지 hello 클러스터에 다른 활성 작업이 있는 경우 실행 작업을 완료 한 후 지정 합니다.<br/><br/>예를 들어 활동 실행 6 분 및 timetolive 않습니다 too5 분, 5 분 후 hello에 대 한 연결 유지 hello 클러스터 유지할 6 분의 처리를 실행 하는 hello 활동을 설정 합니다. Hello에서 처리 된를 실행 하는 다른 활동을 hello 6 분 동안 창을 실행 하는 경우 동일한 클러스터입니다.<br/><br/>주문형 HDInsight 클러스터를 만드는 작업은 비용이 많이 드는 작업 (이 걸릴 수), 따라서 데이터 팩터리의 필요한 tooimprove 성능으로이 설정을 사용 하 여 주문형 HDInsight 클러스터를 다시 사용 하 여 합니다.<br/><br/>Timetolive 값 too0로 설정 하면 hello 클러스터 hello 활동이 실행 완료 되는 즉시 삭제 됩니다. 반면, 높은 값을 설정 하는 경우 hello 클러스터 불필요 하 게 많은 비용이 발생 유휴 유지 될 수 있습니다. 따라서이 필요에 따라 hello 적절 한 값을 설정 하는 중요 합니다.<br/><br/>Hello timetolive 속성 값을 적절 하 게 설정 하는 경우 여러 파이프라인 hello 주문형 HDInsight 클러스터의 hello 인스턴스를 공유할 수 있습니다.  |예 |
| 버전 |Hello HDInsight 클러스터의 버전입니다. hello은 Windows 클러스터에 대 한 3.1 및 3.2 Linux 클러스터에 대 한 |아니요 |
| linkedServiceName | Azure 저장소 연결 서비스 toobe를 저장 하 고 데이터 처리에 대 한 hello 주문형 클러스터에서 사용 합니다. hello HDInsight 클러스터를 만드는 hello에 동일한 Azure 저장소 계정과이 지역입니다.<p>현재, hello 저장소로 Azure 데이터 레이크 저장소를 사용 하는 주문형 HDInsight 클러스터를 만들 수 없습니다. Azure 데이터 레이크 저장소에서 처리 하는 HDInsight에서 toostore hello 결과 데이터를 원하는 hello Azure Blob 저장소 toohello Azure 데이터 레이크 저장소에서에서 복사 작업 toocopy hello 데이터를 사용 합니다. </p>  | 예 |
| additionalLinkedServiceNames |HDInsight hello에 대 한 추가 저장소 계정을 연결 된 서비스 hello 데이터 팩터리 서비스에서 사용자 대신 등록할 수 있도록 지정 합니다. 이러한 저장소 계정은 hello에 있어야에서 생성 된 hello 동일 hello HDInsight 클러스터와 동일한 지역 hello 저장소 계정과 linkedServiceName로 지정 된 지역입니다. |아니요 |
| osType |운영 체제 유형입니다. 허용되는 값은 Windows(기본값) 및 Linux입니다. |아니요 |
| hcatalogLinkedServiceName |Azure SQL 연결의 hello 이름에 해당 지점 toohello HCatalog 데이터베이스를 서비스입니다. hello 주문형 HDInsight 클러스터는 hello metastore로 hello Azure SQL 데이터베이스를 사용 하 여 생성 됩니다. |아니요 |

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON 예제

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>고급 속성
또한 hello 다음과 같은 hello 주문형 HDInsight 클러스터의 hello 세분화 된 구성에 대 한 속성을 지정할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| coreConfiguration |Hello HDInsight 클러스터 toobe 생성에 대 한 hello 핵심 구성 매개 변수 (예: 핵심 site.xml)를 지정 합니다. |아니요 |
| hBaseConfiguration |Hello HBase 구성 매개 변수 (hbase-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| hdfsConfiguration |Hello HDFS 구성 매개 변수 (hdfs-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| hiveConfiguration |Hello hive 구성 매개 변수 (hive-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| mapReduceConfiguration |Hello MapReduce 구성 매개 변수 (mapred-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| oozieConfiguration |Hello Oozie 구성 매개 변수 (oozie-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| stormConfiguration |Hello Storm 구성 매개 변수 (storm-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |
| yarnConfiguration |Hello Yarn 구성 매개 변수 (yarn-site.xml) hello HDInsight 클러스터에 대 한을 지정합니다. |아니요 |

#### <a name="example--on-demand-hdinsight-cluster-configuration-with-advanced-properties"></a>예제 - 고급 속성을 포함하는 주문형 HDInsight 클러스터 구성

```json
{
  "name": " HDInsightOnDemandLinkedService",
  "properties": {
    "type": "HDInsightOnDemand",
    "typeProperties": {
      "clusterSize": 16,
      "timeToLive": "01:30:00",
      "linkedServiceName": "adfods1",
      "coreConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "hiveConfiguration": {
        "templeton.mapper.memory.mb": "5000"
      },
      "mapReduceConfiguration": {
        "mapreduce.reduce.java.opts": "-Xmx4000m",
        "mapreduce.map.java.opts": "-Xmx4000m",
        "mapreduce.map.memory.mb": "5000",
        "mapreduce.reduce.memory.mb": "5000",
        "mapreduce.job.reduce.slowstart.completedmaps": "0.8"
      },
      "yarnConfiguration": {
        "yarn.app.mapreduce.am.resource.mb": "5000",
        "mapreduce.map.memory.mb": "5000"
      },
      "additionalLinkedServiceNames": [
        "datafeeds",
        "adobedatafeed"
      ]
    }
  }
}
```

### <a name="node-sizes"></a>노드 크기
다음과 같은 속성 hello를 사용 하 여 h e a d, 데이터 및 사육 노드의 hello 크기를 지정할 수 있습니다. 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| headNodeSize |Hello hello 헤드 노드 크기를 지정 합니다. hello 기본값은: Standard_D3 합니다. Hello 참조 **노드 크기를 지정** 자세한 내용은 섹션. |아니요 |
| dataNodeSize |Hello 데이터 노드의 hello 크기를 지정합니다. hello 기본값은: Standard_D3 합니다. |아니요 |
| zookeeperNodeSize |Hello Zoo 키퍼 노드의 hello 크기를 지정합니다. hello 기본값은: Standard_D3 합니다. |아니요 |

#### <a name="specifying-node-sizes"></a>노드 크기 지정
Hello 참조 [가상 컴퓨터의 크기](../virtual-machines/linux/sizes.md) toospecify hello 이전 섹션에서 언급 한 hello 속성에 대 한 해야 하는 문자열 값에 대 한 문서입니다. hello 값 필요 tooconform toohello **Cmdlet 및 API** hello 문서에서 참조 합니다. Hello 문서의 보시 Large (기본값) 크기의 데이터 노드가 hello 시나리오에는 충분 하지 않을 수 있는 7 GB 메모리를 있습니다. 

D4 toocreate 작업자 노드 및 헤드 노드 크기를 지정 **Standard_D4** headNodeSize 및 dataNodeSize 속성에 대 한 hello 값으로. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

이러한 속성에 대 한 잘못 된 값을 지정 하면 hello 다음 나타날 수 있습니다 **오류:** toocreate 클러스터 실패 합니다. 예외: 수 없습니다 toocomplete hello 클러스터 만들기 작업입니다. 작업이 실패했습니다. 오류 코드는 '400'입니다. 클러스터의 상태가 '오류'로 남아 있습니다. 메시지: 'PreClusterCreationValidationFailure'. 이 오류를 받으면 hello를 사용 하 고 있는지 확인 **CMDLET 및 API** hello hello 테이블에서 이름이 [가상 컴퓨터의 크기](../virtual-machines/linux/sizes.md) 문서.  

## <a name="bring-your-own-compute-environment"></a>사용자 고유의 계산 환경 가져오기
이 구성의 형식에서는 사용자가 이미 기존 컴퓨팅 환경을 데이터 팩터리에서 연결된 서비스로 등록할 수 있습니다. hello 컴퓨팅 환경을 hello 사용자에 의해 관리 되는 데이터 팩터리 서비스 hello 사용 tooexecute hello 활동 합니다.

이러한 유형의 구성 계산 환경 hello에서 다음에 대해 사용할 수 있습니다.

* Azure HDInsight
* Azure 배치
* Azure 기계 학습
* Azure 데이터 레이크 분석
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스
데이터 팩터리에 Azure HDInsight 연결 된 서비스 tooregister 고유한 HDInsight 클러스터를 만들 수 있습니다.

### <a name="example"></a>예제

```json
{
  "name": "HDInsightLinkedService",
  "properties": {
    "type": "HDInsight",
    "typeProperties": {
      "clusterUri": " https://<hdinsightclustername>.azurehdinsight.net/",
      "userName": "admin",
      "password": "<password>",
      "linkedServiceName": "MyHDInsightStoragelinkedService"
    }
  }
}
```

### <a name="properties"></a>속성
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**HDInsight**합니다. |예 |
| clusterUri |hello hello HDInsight 클러스터의 URI입니다. |예 |
| username |Tooconnect tooan 기존 HDInsight 클러스터를 사용 하는 hello 사용자 toobe의 hello 이름을 지정 합니다. |예 |
| 암호 |Hello 사용자 계정의 암호를 지정 합니다. |예 |
| linkedServiceName | Hello HDInsight 클러스터의 hello toohello Azure blob 저장소를 참조 하는 Azure 저장소 연결 서비스의 이름을 사용 합니다. <p>현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다. Hello HDInsight 클러스터에 데이터 레이크 저장소 액세스 toohello 경우 Hive/Pig 스크립트에서 hello Azure 데이터 레이크 저장소의에서 데이터를 액세스할 수 있습니다. </p>  |예 |

## <a name="azure-batch-linked-service"></a>Azure 일괄 처리 연결된 서비스
Azure 배치 연결 서비스 tooregister 가상 컴퓨터 (Vm) tooa 데이터 팩터리의 일괄 처리 풀을 만들 수 있습니다. Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.

새 tooAzure 일괄 처리 서비스는 경우 다음 항목을 참조 하십시오.

* [Azure 배치 기본 사항](../batch/batch-technical-overview.md) hello Azure 배치 서비스에 대 한 개요입니다.
* [New-azurebatchaccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet toocreate Azure 배치 계정 (또는) [Azure 포털](../batch/batch-account-create-portal.md) toocreate hello Azure 배치 계정을 Azure 포털을 사용 합니다. 참조 [PowerShell 사용 하 여 Azure 배치 계정 toomanage](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) hello cmdlet을 사용 하는 자세한 방법은 대 한 항목입니다.
* [New-azurebatchpool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet toocreate Azure 배치 풀 합니다.

### <a name="example"></a>예제

```json
{
  "name": "AzureBatchLinkedService",
  "properties": {
    "type": "AzureBatch",
    "typeProperties": {
      "accountName": "<Azure Batch account name>",
      "accessKey": "<Azure Batch account key>",
      "poolName": "<Azure Batch pool name>",
      "linkedServiceName": "<Specify associated storage linked service reference here>"
    }
  }
}
```

추가 "**.\< 지역 이름\>**"hello에 대 한 일괄 처리 계정 이름을 toohello **accountName** 속성입니다. 예제:

```json
"accountName": "mybatchaccount.eastus"
```

두 번째 방법은 tooprovide hello batchUri 끝점 hello 다음 예제와 같이:

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>properties
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |너무 hello 유형 속성을 설정 해야**AzureBatch**합니다. |예 |
| accountName |Azure 배치 계정 hello의 이름입니다. |예 |
| accessKey |Hello Azure 배치 계정에 대 한 액세스 키입니다. |예 |
| poolName |가상 컴퓨터의 hello 풀의 이름입니다. |예 |
| linkedServiceName |Hello이 Azure 배치 연결 된 서비스와 연결 된 Azure 저장소 연결 서비스의 이름입니다. 준비 파일에 대 한이 연결 된 서비스는 필요한 toorun hello 활동 및 hello 활동 실행 로그를 저장 합니다. |예 |

## <a name="azure-machine-learning-linked-service"></a>Azure 기계 학습 연결된 서비스
Azure 기계 학습 연결 서비스 tooregister를 끝점 tooa 데이터 팩터리 점수 매기기 기계 학습 일괄 만듭니다.

### <a name="example"></a>예제

```json
{
  "name": "AzureMLLinkedService",
  "properties": {
    "type": "AzureML",
    "typeProperties": {
      "mlEndpoint": "https://[batch scoring endpoint]/jobs",
      "apiKey": "<apikey>"
    }
  }
}
```

### <a name="properties"></a>속성
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| 형식 |hello type 속성이로 설정 해야: **AzureML**합니다. |예 |
| mlEndpoint |hello 일괄 처리 첨 수 매기기 URL입니다. |예 |
| apiKey |hello 작업 영역 모델의 API를 게시 합니다. |예 |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure 데이터 레이크 분석 연결된 서비스
만들 프로그램 **Azure 데이터 레이크 분석** 서비스 toolink Azure Data Lake 분석 계산 서비스 tooan Azure 데이터 팩터리에 연결 합니다. 데이터 레이크 분석 U-SQL 작업 hello 파이프라인의 hello toothis 연결 된 서비스를 참조합니다. 

hello 다음 표에서 hello에 대 한 설명을 hello JSON 정의에서 사용 되는 일반 속성. 서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| **type** |hello type 속성이로 설정 해야: **AzureDataLakeAnalytics**합니다. |예 |
| **accountName** |Azure 데이터 레이크 분석 계정 이름입니다. |예 |
| **dataLakeAnalyticsUri** |Azure 데이터 레이크 분석 URI입니다. |아니요 |
| **subscriptionId** |Azure 구독 ID |아니요 (지정 하지 않으면 데이터 팩터리에 사용 되는 hello의 구독) 하는 경우. |
| **resourceGroupName** |Azure 리소스 그룹 이름 |아니요 (지정 하지 않으면 리소스 그룹의 데이터 팩터리에 사용 되는 hello) 하는 경우. |

### <a name="service-principal-authentication-recommended"></a>서비스 주체 인증(권장)
toouse 서비스 보안 주체 인증 레지스터 것 hello Azure Active Directory (Azure AD) 및 권한 부여의 응용 프로그램 엔터티 tooData 레이크 스토어에 액세스 합니다. 자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요. 사용 되는 값을 다음 hello 기록 toodefine hello 연결 된 서비스:
* 응용 프로그램 UI
* 응용 프로그램 키 
* 테넌트 ID

Hello 다음과 같은 속성을 지정 하 여 서비스 사용자 인증을 사용 합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **servicePrincipalId** | Hello 응용 프로그램의 클라이언트 ID를 지정 | 예 |
| **servicePrincipalKey** | Hello 응용 프로그램의 키를 지정 합니다. | 예 |
| **테넌트** | 응용 프로그램에 속한 아래 hello 테 넌 트 정보 (도메인 이름 또는 테 넌 트 ID)를 지정 합니다. Hello Azure 포털의 오른쪽 위 모서리 hello에에서 hello 마우스 호버 하 여 검색할 수 있습니다. | 예 |

**예제: 서비스 주체 인증**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>사용자 자격 증명 인증
또는 hello 다음과 같은 속성을 지정 하 여 Data Lake 분석에 대 한 사용자 자격 증명 인증을 사용할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **권한 부여** | Hello 클릭 **Authorize** hello 데이터 팩터리 편집기 단추를 선택한 hello 자동 생성 된 권한 부여 URL toothis 속성을 할당 하 여 자격 증명을 입력 합니다. | 예 |
| **sessionId** | Hello OAuth 권한 부여 세션에서 OAuth 세션 ID입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있습니다. 이 설정은 hello 데이터 팩터리 편집기를 사용 하는 경우 자동으로 생성 됩니다. | 예 |

**예제: 사용자 자격 증명 인증**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "datalakeanalyticscompute.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>토큰 만료
hello를 사용 하 여 생성 하는 인증 코드를 hello **Authorize** 단추 잠시 후에 만료 됩니다. 다음 표에 다양 한 유형의 사용자 계정에 대 한 만료 시간 hello에 대 한 hello를 참조 하십시오. Hello 다음과 같은 오류 메시지가 표시 될 수 있습니다 때 인증 hello **토큰이 만료 된**: 작업 오류를 자격 증명: invalid_grant-AADSTS70002: 자격 증명 유효성 검사 오류입니다. AADSTS70008: hello 액세스 권한 부여가 만료 되었거나 해지 제공 합니다. 추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z

| 사용자 유형 | 다음 시간 후에 만료 |
|:--- |:--- |
| Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등) |12시간 |
| AAD(Azure Active Directory)에서 관리되는 사용자 계정 |hello 마지막 조각 실행 한 후 14 일입니다. <br/><br/>OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일 |

tooavoid/resolve이 오류를 hello를 사용 하 여 권한을 다시 부여 **Authorize** 때 hello 단추 **토큰이 만료 되** hello 연결 된 서비스를 다시 배포 합니다. 다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

참조 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 세부 정보에 대 한 항목 hello Data Factory 클래스 hello 코드에 사용 정보 합니다. 에 대 한 참조 추가: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll hello WindowsFormsWebAuthenticationDialog 클래스에 대 한 합니다. 

## <a name="azure-sql-linked-service"></a>Azure SQL 연결된 서비스
Azure SQL 연결 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="azure-sql-data-warehouse-linked-service"></a>Azure SQL Data Warehouse 연결된 서비스
Azure SQL 데이터 웨어하우스 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 이 연결된 서비스에 대한 자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="sql-server-linked-service"></a>SQL Server 연결된 서비스
SQL Server 연결 된 서비스를 만들고 사용 하 여 hello로 [저장 프로시저 작업](data-factory-stored-proc-activity.md) tooinvoke 데이터 팩토리 파이프라인에서 저장된 프로시저입니다. 이 연결된 서비스에 대한 자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.

