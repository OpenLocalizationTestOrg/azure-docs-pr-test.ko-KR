---
title: "Azure Data Factory에서 지원하는 컴퓨팅 환경 | Microsoft Docs"
description: "데이터의 변환 또는 처리를 위해 Azure Data Factory 파이프라인(예: Azure HDInsight)에서 사용할 수 있는 계산 환경을 알아봅니다."
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
ms.openlocfilehash: da7110614e684656da3ef9830780606e1576684d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="compute-environments-supported-by-azure-data-factory"></a>Azure Data Factory에서 지원하는 컴퓨팅 환경
이 문서는 프로세스 또는 변환 데이터에 사용할 수 있는 다양한 계산 환경을 설명합니다. 또한 이러한 계산 환경을 Azure 데이터 팩터리에 연결하는 연결된 서비스를 구성하는 경우 데이터 팩터리에서 지원하는 다른 구성(주문형 vs. 사용자 고유)에 대한 자세한 내용을 제공합니다.

다음 표는 Data Factory 및 실행할 수 있는 작업에서 지원하는 컴퓨팅 환경 목록을 제공합니다. 

| 컴퓨팅 환경 | 작업 |
| --- | --- |
| [주문형 HDInsight 클러스터](#azure-hdinsight-on-demand-linked-service) 또는 [사용자 고유의 HDInsight 클러스터](#azure-hdinsight-linked-service) |[DotNet](data-factory-use-custom-activities.md), [Hive](data-factory-hive-activity.md), [Pig](data-factory-pig-activity.md), [MapReduce](data-factory-map-reduce.md), [Hadoop 스트리밍](data-factory-hadoop-streaming-activity.md) |
| [Azure 배치](#azure-batch-linked-service) |[DotNet](data-factory-use-custom-activities.md) |
| [Azure 기계 학습](#azure-machine-learning-linked-service) |[Machine Learning 작업: 배치 실행 및 업데이트 리소스](data-factory-azure-ml-batch-execution-activity.md) |
| [Azure 데이터 레이크 분석](#azure-data-lake-analytics-linked-service) |[데이터 레이크 분석 U-SQL](data-factory-usql-activity.md) |
| [Azure SQL](#azure-sql-linked-service), [Azure SQL Data Warehouse](#azure-sql-data-warehouse-linked-service), [SQL Server](#sql-server-linked-service) |[저장 프로시저](data-factory-stored-proc-activity.md) |

## <a name="supported-hdinsight-versions-in-azure-data-factory"></a>Azure Data Factory에서 지원되는 HDInsight 버전
Azure HDInsight는 언제든 배포할 수 있는 여러 Hadoop 클러스터 버전을 지원합니다. 각 버전을 선택하면 특정 버전의 HDP(Hortonworks Data Platform) 배포 및 배포에 포함된 구성 요소 집합이 만들어집니다. Microsoft는 지원되는 HDInsight 버전 목록을 계속 업데이트하여 최신 Hadoop 에코시스템 구성 요소 및 수정 프로그램을 제공합니다. HDInsight 3.2는 2017년 4월 1일부터 사용되지 않습니다. 자세한 내용은 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)을 참조하세요.

이로 인해 HDInsight 3.2 클러스터에 대해 실행되는 활동이 있는 기존 Azure Data Factory에 영향을 미칩니다. 영향을 받는 Data Factory를 업데이트하려면 사용자는 다음 섹션의 지침을 따르는 것이 좋습니다.

### <a name="for-linked-services-pointing-to-your-own-hdinsight-clusters"></a>사용자 고유의 HDInsight 클러스터를 가리키는 연결된 서비스의 경우
* **사용자 고유의 HDInsight 3.2 이하 클러스터를 가리키는 HDInsight 연결된 서비스:**

  Azure Data Factory는 HDI 3.1에서 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)까지 사용자 고유의 HDInsight 클러스터에 제출하는 작업을 지원합니다. 그러나 [지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)에서 설명하는 사용 중단 정책에 따라 2017년 4월 1일 이후로는 더 이상 HDInsight 3.2 클러스터를 만들 수 없습니다.  

  **권장 사항:** 
  * 이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.
  * HDInsight 3.2 클러스터를 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업그레이드하여 최신 Hadoop 에코시스템 구성 요소 및 수정 프로그램을 얻습니다. 

* **사용자 고유의 HDInsight 3.3 이상의 클러스터를 가리키는 HDInsight 연결된 서비스:**

  Azure Data Factory는 HDI 3.1에서 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)까지 사용자 고유의 HDInsight 클러스터에 제출하는 작업을 지원합니다. 
  
  **권장 사항:** 
  * Data Factory 관점에서 보면 아무런 작업도 필요하지 않습니다. 그러나 하위 버전의 HDInsight를 사용하는 경우에도 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업그레이드하여 최신 Hadoop 생태계 구성 요소 및 수정 프로그램을 얻는 것이 좋습니다.

### <a name="for-hdinsight-on-demand-linked-services"></a>주문형 HDInsight 연결된 서비스의 경우
* **주문형 HDInsight 연결된 서비스 JSON 정의에 지정되어 있는 버전 3.2 이하:**
  
  Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다. 기존의 주문형 HDInsight 3.2 연결된 서비스에 대한 지원 종료는 **2017년 7월 15일**까지로 연장됩니다.  

  **권장 사항:** 
  * 이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.
  * **2017년 7월 15일** 이전까지 주문형 HDI 연결된 서비스 JSON 정의의 Version 속성을 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)으로 업데이트하여 최신 Hadoop 생태계 구성 요소 및 수정 프로그램을 얻습니다. JSON 정의에 대한 자세한 내용은 [주문형 Azure HDInsight 연결된 서비스 샘플](#azure-hdinsight-on-demand-linked-service)을 참조하세요. 

* **주문형 HDInsight 연결된 서비스에 지정되지 않은 버전:**
  
  Azure Data Factory에서는 **2017년 5월 15일**부터 버전 3.3 이상의 주문형 HDInsight 클러스터 만들기를 지원합니다. 기존의 주문형 HDInsight 3.2 연결된 서비스에 대한 지원 종료는 **2017년 7월 15일**까지로 연장됩니다. 

  **2017년 7월 15일** 이전까지 version 및 osType 속성의 값을 비워 두는 경우 해당 속성의 기본값은 다음과 같습니다. 

  | 속성 | 기본값 | 필수 |
  | --- | --- | --- |
  버전   | Windows 클러스터용 HDI 3.1 및 Linux 클러스터용 HDI 3.2| 아니요
  osType | 기본값: Windows | 아니요

  **2017년 7월 15일** 이후 version 및 osType 속성의 값을 비워 두는 경우 해당 속성의 기본값은 다음과 같습니다.

  | 속성 | 기본값 | 필수 |
  | --- | --- | --- |
  버전   | Windows 클러스터용 HDI 3.3 및 Linux 클러스터용 3.5.    | 아니요
  osType | 기본값: Linux | 아니요

  **권장 사항:** 
  * **2017년 7월 15일** 이전까지 이 연결된 서비스를 참조하는 활동과 [최신의 지원되는 HDInsight 버전](../hdinsight/hdinsight-component-versioning.md#supported-hdinsight-versions)의 호환성을 보장하기 위해 [각 HDInsight 버전에서 제공되는 Hadoop 구성 요소](../hdinsight/hdinsight-component-versioning.md#hadoop-components-available-with-different-hdinsight-versions) 및 [HDInsight 버전과 관련된 Hortonworks 릴리스 정보](../hdinsight/hdinsight-component-versioning.md#hortonworks-release-notes-associated-with-hdinsight-versions)에서 설명하는 정보와 함께 테스트를 수행합니다.  
  * **2017년 7월 15일** 이후 기본 설정을 재정의하려는 경우 osType 및 버전 값을 명시적으로 지정해야 합니다. 

>[!Note]
>현재 Azure Data Factory는 Azure Data Lake Store를 기본 저장소로 사용하는 HDInsight 클러스터를 지원하지 않습니다. Azure Storage를 HDInsight 클러스터의 기본 저장소로 사용합니다. 
>  
>  

## <a name="on-demand-compute-environment"></a>주문형 계산 환경
이 구성의 형식에서는 컴퓨팅 환경은 Azure 데이터 팩터리 서비스에 의해 완벽하게 관리됩니다. 데이터를 처리하기 위한 작업을 제출하기 전에 데이터 팩터리 서비스에서 자동으로 컴퓨팅 환경을 만들고 작업이 완료되면 제거합니다. 사용자는 주문형 계산 환경에 대한 연결된 서비스를 만들고 구성하며 작업 실행, 클러스터 관리, 부트스트래핑 작업에 대한 세부적인 설정을 제어할 수 있습니다.

> [!NOTE]
> 주문형 구성은 현재 Azure HDInsight 클러스터에 대해서만 지원됩니다.
> 
> 

## <a name="azure-hdinsight-on-demand-linked-service"></a>Azure HDInsight 주문형 연결된 서비스
Azure 데이터 팩터리 서비스는 데이터를 처리하는 Windows/Linux 기반 주문형 HDInsight 클러스터를 자동으로 만들 수 있습니다. 클러스터는 클러스터와 연결된 저장소 계정(JSON에서 linkedServiceName 속성)과 동일한 하위 지역에 만들어집니다. 저장소 계정은 범용 표준 Azure Storage 계정이어야 합니다. 

주문형 HDInsight 연결된 서비스에 대해 다음 **중요한** 점에 유의하십시오.

* Azure 구독에서 만든 주문형 HDInsight 클러스터는 표시되지 않습니다. Azure 데이터 팩터리 서비스는 사용자를 대신해 주문형 HDInsight 클러스터를 관리합니다.
* 주문형 HDInsight 클러스터에서 실행하는 작업에 대한 로그는 HDInsight 클러스터와 연결된 저장소 계정에 복사됩니다. **작업 실행 세부 정보** 블레이드의 Azure 포털에서 이러한 로그에 액세스할 수 있습니다. 세부 정보는 [파이프라인 모니터링 및 관리](data-factory-monitor-manage-pipelines.md) 문서를 참조하십시오.
* HDInsight 클러스터가 작업을 실행 중인 경우에 대해서만 청구됩니다.

> [!IMPORTANT]
> 주문형 Azure HDInsight 클러스터를 프로비전하는 데 일반적으로 **20분** 이상이 걸립니다.
> 
> 

### <a name="example"></a>예
다음 JSON는 Linux 기반 주문형 HDInsight 연결된 서비스를 정의합니다. Data Factory 서비스는 데이터 조각을 처리하는 경우 **Linux 기반** HDInsight 클러스터를 자동으로 만듭니다. 

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

Windows 기반 HDInsight 클러스터를 사용하려면 **osType**을 **windows**로 설정하거나 기본값(windows)으로 속성을 사용하지 않습니다.  

> [!IMPORTANT]
> HDInsight 클러스터는 JSON(**linkedServiceName**)에서 지정한 Blob Storage에 **기본 컨테이너**를 만듭니다. HDInsight는 클러스터가 삭제될 때 이 컨테이너를 삭제하지 않습니다. 이 동작은 의도된 것입니다. 주문형 HDInsight 연결된 서비스에서는 기존 라이브 클러스터(**timeToLive**)가 없는 한 슬라이스를 처리해야 할 때마다 HDInsight 클러스터가 만들어지며 처리가 완료되면 삭제됩니다. 
> 
> 많은 조각이 처리될수록 Azure Blob Storage에 컨테이너가 많아집니다. 작업의 문제 해결을 위해 이 항목들이 필요하지 않다면 저장소 비용을 줄이기 위해 삭제할 수 있습니다. 이러한 컨테이너의 이름은 `adf**yourdatafactoryname**-**linkedservicename**-datetimestamp` 패턴을 따릅니다. [Microsoft 저장소 탐색기](http://storageexplorer.com/) 같은 도구를 사용하여 Azure Blob Storage에서 컨테이너를 삭제합니다.
> 
> 

### <a name="properties"></a>속성
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |형식 속성은 **HDInsightOnDemand**로 설정해야 합니다. |예 |
| clusterSize |클러스터의 작업자/데이터 노드 수 HDInsight 클러스터는 속성에 지정한 작업자 노드의 수와 함께 2개의 헤드 노드로 생성됩니다. 노드의 크기는 4개 코어를 포함한 Standard_D3이므로, 4개 작업자 노드 클러스터에서 24개 코어(작업자 노드용 4\*4 = 16코어 및 헤드 노드용 2\*4 = 8코어)를 사용합니다. Standard_D3 계층에 대한 자세한 내용은 [HDInsight에서 Linux 기반 Hadoop 클러스터 만들기](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md)를 참조하세요. |예 |
| timetolive |주문형 HDInsight 클러스터에 대한 허용된 유휴 시간입니다. 클러스터에 다른 활성 작업이 없으면 작업이 완료된 후에 주문형 HDInsight 클러스터가 유지될 기간을 지정합니다.<br/><br/>예를 들어 활동 실행에 6분이 걸리고 timetolive이 5분으로 설정된 경우 클러스터는 활동을 처리하는 6분 동안 실행된 후에 5분 동안 유지됩니다. 다른 활동 실행이 6분 창을 실행하는 경우 동일한 클러스터에 의해 처리됩니다.<br/><br/>주문형 HDInsight 클러스터를 만드는 데는 많은 시간이 걸려 값 비싼 작업이 되므로 필요할 때마다 이 설정을 사용하여 주문형 HDInsight 클러스터를 다시 사용함으로써 데이터 팩터리의 성능을 향상시킵니다.<br/><br/>timetolive 값을 0으로 설정한 경우 클러스터는 작업 실행이 완료되는 즉시 삭제됩니다. 반면 높은 값을 설정하는 경우 클러스터는 불필요하게 많은 비용이 발생하는 유휴 상태에 머무를 수 있습니다. 따라서 필요에 따라 적절한 값을 설정하는 것이 중요합니다.<br/><br/>timetolive 속성 값이 적절하게 설정되는 경우 여러 파이프라인은 주문형 HDInsight 클러스터의 인스턴스를 공유할 수 있습니다.  |예 |
| 버전 |HDInsight 클러스터의 버전입니다. 기본값은 Windows 클러스터의 경우 3.1이고 Linux 클러스터의 경우 3.2입니다. |아니요 |
| linkedServiceName | 데이터를 저장 및 처리하기 위해 주문형 클러스터에서 사용하는 Azure Storage 연결 서비스입니다. HDInsight 클러스터는 Azure Storage 계정과 동일한 지역에 생성됩니다.<p>현재 Azure Data Lake Store를 저장소로 사용하는 주문형 HDInsight 클러스터를 만들 수 없습니다. HDInsight 처리의 결과 데이터를 Azure Data Lake Store에 저장하려면 복사 작업을 사용하여 Azure Blob Storage의 데이터를 Azure Data Lake Store로 복사합니다. </p>  | 예 |
| additionalLinkedServiceNames |HDInsight 연결된 서비스에 대한 추가 저장소 계정을 지정하므로 데이터 팩터리 서비스가 사용자를 대신해 계정을 등록할 수 있습니다.  이러한 저장소 계정은 linkedServiceName에 지정된 저장소 계정과 동일한 지역에 생성된 HDInsight 클러스터와 동일한 지역에 있어야 합니다. |아니요 |
| osType |운영 체제 유형입니다. 허용되는 값은 Windows(기본값) 및 Linux입니다. |아니요 |
| hcatalogLinkedServiceName |HCatalog 데이터베이스를 가리키는 Azure SQL 연결된 서비스 이름입니다. 주문형 HDInsight 클러스터는 Azure SQL Database를 metastore로 사용하여 만들어집니다. |아니요 |

#### <a name="additionallinkedservicenames-json-example"></a>additionalLinkedServiceNames JSON 예제

```json
"additionalLinkedServiceNames": [
    "otherLinkedServiceName1",
    "otherLinkedServiceName2"
  ]
```

### <a name="advanced-properties"></a>고급 속성
또한 주문형 HDInsight 클러스터의 세부적인 구성에 다음 속성을 지정할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| coreConfiguration |만들어지는 HDInsight 클러스터에 대한 핵심 구성 매개 변수(core-site.xml에서 처럼)를 지정합니다. |아니요 |
| hBaseConfiguration |HDInsight 클러스터에 대한 HBase 구성 매개 변수(hbase-site.xml)를 지정합니다. |아니요 |
| hdfsConfiguration |HDInsight 클러스터에 대한 HDFS 구성 매개 변수(hdfs-site.xml)를 지정합니다. |아니요 |
| hiveConfiguration |HDInsight 클러스터에 대한 hive 구성 매개 변수(hive-site.xml)를 지정합니다. |아니요 |
| mapReduceConfiguration |HDInsight 클러스터에 대한 MapReduce 구성 매개 변수(mapred-site.xml)를 지정합니다. |아니요 |
| oozieConfiguration |HDInsight 클러스터에 대한 Oozie 구성 매개 변수(oozie-site.xml)를 지정합니다. |아니요 |
| stormConfiguration |HDInsight 클러스터에 대한 Storm 구성 매개 변수(storm-site.xml)를 지정합니다. |아니요 |
| yarnConfiguration |HDInsight 클러스터에 대한 Yarn 구성 매개 변수(yarn-site.xml)를 지정합니다. |아니요 |

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
다음 속성을 사용하여 헤드, 데이터 및 Zookeeper 노드의 크기를 지정할 수 있습니다. 

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| headNodeSize |헤드 노드의 크기를 지정합니다. 기본값은 Standard_D3입니다. 자세한 내용은 **노드 크기 지정** 섹션을 참조하세요. |아니요 |
| dataNodeSize |데이터 노드의 크기를 지정합니다. 기본값은 Standard_D3입니다. |아니요 |
| zookeeperNodeSize |Zookeeper 노드의 크기를 지정합니다. 기본값은 Standard_D3입니다. |아니요 |

#### <a name="specifying-node-sizes"></a>노드 크기 지정
이전 섹션에 언급된 속성에 대해 지정해야 하는 문자열 값은 [가상 컴퓨터 크기](../virtual-machines/linux/sizes.md) 문서를 참조하세요. 값은 이 문서에서 참조된 **Cmdlet 및 API**를 준수해야 합니다. 이 문서에서 볼 수 있는 것처럼 크게(기본값) 크기의 데이터 노드는 메모리가 7GB이므로 시나리오에 맞지 않을 수 있습니다. 

D4 크기의 헤드 노드 및 작업자 노드를 만들려는 경우 headNodeSize 및 dataNodeSize 속성에 대한 값으로 **Standard_D4**를 지정합니다. 

```json
"headNodeSize": "Standard_D4",    
"dataNodeSize": "Standard_D4",
```

이러한 속성에 잘못된 값을 지정하는 경우 다음과 같은 오류가 발생할 수 있습니다. **오류:** 클러스터를 만들지 못했습니다. 예외: 클러스터 만들기 작업을 완료할 수 없습니다. 작업이 실패했습니다. 오류 코드는 '400'입니다. 클러스터의 상태가 '오류'로 남아 있습니다. 메시지: 'PreClusterCreationValidationFailure'. 이 오류가 발생하면 [가상 컴퓨터 크기](../virtual-machines/linux/sizes.md) 문서의 테이블에서 **CMDLET 및 API** 이름을 사용하고 있는지 확인합니다.  

## <a name="bring-your-own-compute-environment"></a>사용자 고유의 계산 환경 가져오기
이 구성의 형식에서는 사용자가 이미 기존 컴퓨팅 환경을 데이터 팩터리에서 연결된 서비스로 등록할 수 있습니다. 컴퓨팅 환경은 이를 사용하여 작업을 실행하는 데이터 팩터리 서비스와 사용자에 의해 관리됩니다.

이 구성의 형식은 다음의 계산 환경에 대해 지원됩니다.

* Azure HDInsight
* Azure 배치
* Azure 기계 학습
* Azure 데이터 레이크 분석
* Azure SQL DB, Azure SQL DW, SQL Server

## <a name="azure-hdinsight-linked-service"></a>Azure HDInsight 연결된 서비스
Azure HDInsight 연결된 서비스를 만들어서 데이터 팩터리를 사용하는 사용자 고유의 HDInsight 클러스터를 등록할 수 있습니다.

### <a name="example"></a>예

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
| type |형식 속성은 **HDInsight**로 설정해야 합니다. |예 |
| clusterUri |HDInsight 클러스터의 URI입니다. |예 |
| username |기존 HDInsight 클러스터에 연결하는데 사용할 사용자의 이름을 지정합니다. |예 |
| password |사용자 계정으로 password를 지정합니다. |예 |
| linkedServiceName | HDInsight 클러스터에서 사용하는 Azure Blob Storage를 참조하는 Azure Storage 연결된 서비스의 이름입니다. <p>현재 이 속성에 대한 Azure Data Lake Store 연결된 서비스를 지정할 수 없습니다. HDInsight 클러스터가 Data Lake Store에 액세스할 경우 Hive/Pig 스크립트의 Azure Data Lake Store에 있는 데이터에 액세스할 수 있습니다. </p>  |예 |

## <a name="azure-batch-linked-service"></a>Azure 일괄 처리 연결된 서비스
Azure 일괄 처리 연결된 서비스를 만들어 데이터 팩터리에 가상 컴퓨터(VM)의 일괄 처리 풀을 등록합니다. Azure 일괄 처리 또는 Azure HDInsight를 사용하여 .NET 사용자 지정 활동을 실행할 수 있습니다.

Azure 배치 서비스가 처음이라면 다음 항목을 참조하십시오.

* [Azure 배치 기본 사항](../batch/batch-technical-overview.md) 입니다.
* Azure 배치 계정을 만드는 [New-AzureBatchAccount](https://msdn.microsoft.com/library/mt125880.aspx) cmdlet 또는 Azure 배치 계정을 만드는 [Azure Portal](../batch/batch-account-create-portal.md). 이 cmdlet 사용에 관한 자세한 지침은 [PowerShell을 사용하여 Azure Batch 계정 관리](http://blogs.technet.com/b/windowshpc/archive/2014/10/28/using-azure-powershell-to-manage-azure-batch-account.aspx) 항목을 참조하십시오.
* [New-AzureBatchPool](https://msdn.microsoft.com/library/mt125936.aspx) cmdlet을 사용하여 Azure 배치 풀을 만듭니다.

### <a name="example"></a>예

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

**accountName** 속성의 배치 계정의 이름에 "**.\<region name\>**"을 추가합니다. 예제:

```json
"accountName": "mybatchaccount.eastus"
```

다른 옵션은 다음 샘플에 표시된 것처럼 batchUri 끝점을 제공하는 것입니다.

```json
"accountName": "adfteam",
"batchUri": "https://eastus.batch.azure.com",
```

### <a name="properties"></a>속성
| 속성 | 설명 | 필수 |
| --- | --- | --- |
| type |형식 속성은 **AzureBatch**로 설정해야 합니다. |예 |
| accountName |Azure Batch 계정의 이름 |예 |
| accessKey |Azure Batch 계정에 대한 선택키 |예 |
| poolName |가상 컴퓨터의 풀 이름입니다. |예 |
| linkedServiceName |Azure 일괄 처리 연결된 서비스와 관련된 Azure 저장소 연결된 서비스의 이름입니다. 이 연결된 서비스는 활동을 실행하는 데 필요한 파일을 스테이징하고 활동 실행 로그를 저장하는 데 사용됩니다. |예 |

## <a name="azure-machine-learning-linked-service"></a>Azure 기계 학습 연결된 서비스
Azure 컴퓨터 학습 연결된 서비스를 만들어 데이터 팩토리에 끝점을 매기는 기계 학습 일괄 처리를 등록합니다. 

### <a name="example"></a>예

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
| type |형식 속성은 **AzureML**로 설정해야 합니다. |예 |
| mlEndpoint |일괄 처리 점수 매기기 URL입니다. |예 |
| apiKey |게시된 작업 영역 모델의 API입니다. |예 |

## <a name="azure-data-lake-analytics-linked-service"></a>Azure 데이터 레이크 분석 연결된 서비스
Azure 데이터 레이크 분석 계산 서비스와 Azure Data Factory에 연결하는 **Azure 데이터 레이크 분석** 연결된 서비스를 만듭니다. 파이프라인에서 데이터 레이크 분석 U-SQL 작업은 이 연결된 서비스를 가리킵니다. 

다음 표에는 JSON 정의에서 사용하는 일반 속성에 대한 설명이 나와 있습니다. 서비스 주체와 사용자 자격 증명 인증 중에서 추가로 선택할 수 있습니다.

| 속성 | 설명 | 필수 |
| --- | --- | --- |
| **type** |type 속성은 **AzureDataLakeAnalytics**로 설정해야 합니다. |예 |
| **accountName** |Azure 데이터 레이크 분석 계정 이름입니다. |예 |
| **dataLakeAnalyticsUri** |Azure 데이터 레이크 분석 URI입니다. |아니요 |
| **subscriptionId** |Azure 구독 ID |아니요(지정하지 않으면 Data Factory의 구독이 사용됨). |
| **resourceGroupName** |Azure 리소스 그룹 이름 |아니요(지정하지 않으면 Data Factory의 리소스 그룹이 사용됨). |

### <a name="service-principal-authentication-recommended"></a>서비스 주체 인증(권장)
서비스 주체 인증을 사용하려면 Azure AD(Azure Active Directory)에서 응용 프로그램 엔터티를 등록한 후 Data Lake Store에서 액세스 권한을 부여합니다. 자세한 단계는 [서비스 간 인증](../data-lake-store/data-lake-store-authenticate-using-active-directory.md)을 참조하세요. 연결된 서비스를 정의하는 데 사용되므로 다음 값을 적어둡니다.
* 응용 프로그램 UI
* 응용 프로그램 키 
* 테넌트 ID

다음 속성을 지정하여 서비스 주체 인증을 사용합니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **servicePrincipalId** | 응용 프로그램의 클라이언트 ID를 지정합니다. | 예 |
| **servicePrincipalKey** | 응용 프로그램의 키를 지정합니다. | 예 |
| **테넌트** | 응용 프로그램이 있는 테넌트 정보(도메인 이름 또는 테넌트 ID)를 지정합니다. Azure Portal의 오른쪽 위 모서리에 마우스를 이동하여 검색할 수 있습니다. | 예 |

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
또는 다음 속성을 지정하여 Data Lake Analytics에 대해 사용자 자격 증명 인증을 사용할 수 있습니다.

| 속성 | 설명 | 필수 |
|:--- |:--- |:--- |
| **권한 부여** | Data Factory 편집기에서 **권한 부여** 단추를 클릭하고 자격 증명을 입력합니다. 그러면 자동 생성된 authorization URL이 이 속성에 할당됩니다. | 예 |
| **sessionId** | OAuth 권한 부여 세션에서 가져온 OAuth 세션 ID입니다. 각 세션 ID는 고유하고 한 번만 사용될 수 있습니다. 이 설정은 Data Factory 편집기를 사용하는 경우 자동으로 생성됩니다. | 예 |

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
**권한 부여** 단추를 사용하여 생성된 인증 코드는 잠시 후 만료됩니다. 다양한 유형의 사용자 계정에 대한 만료 시간은 다음 표를 참조하세요. 인증 **토큰이 만료**되는 경우 다음과 같은 오류 메시지가 표시될 수 있습니다. 자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명 유효성 검사 오류. "자격 증명 작업 오류: invalid_grant - AADSTS70002: 자격 증명의 유효성 검사 오류 AADSTS70008: 제공된 액세스 권한 부여가 만료되었거나 해지됩니다. 추적 ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 상관관계 ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 타임스탬프: 2015-12-15 21:09:31Z

| 사용자 유형 | 다음 시간 후에 만료 |
|:--- |:--- |
| Azure Active Directory에서 관리되지 않는 사용자 계정(@hotmail.com, @live.com 등) |12시간 |
| AAD(Azure Active Directory)에서 관리되는 사용자 계정 |마지막 조각이 실행된 후 14일 <br/><br/>OAuth 기반 연결된 서비스를 기반으로 하는 조각이 14일마다 한 번 이상 실행된 경우 90일 |

이 오류를 방지/해결하려면 **토큰이 만료**되면 **권한 부여** 단추를 사용하여 다시 인증하고 연결된 서비스를 다시 배포합니다. 다음과 같은 코드를 사용하여 프로그래밍 방식으로 **sessionId** 및 **권한 부여** 속성의 값을 생성할 수도 있습니다.

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

코드에 사용되는 Data Factory 클래스에 대한 세부 정보는 [AzureDataLakeStoreLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx) 및 [AuthorizationSessionGetResponse 클래스](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) 항목을 참조하세요. WindowsFormsWebAuthenticationDialog 클래스의 Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll에 대한 참조를 추가합니다. 

## <a name="azure-sql-linked-service"></a>Azure SQL 연결된 서비스
Azure SQL 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다. 이 연결된 서비스에 대한 자세한 내용은 [Azure SQL 커넥터](data-factory-azure-sql-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="azure-sql-data-warehouse-linked-service"></a>Azure SQL Data Warehouse 연결된 서비스
Azure SQL Data Warehouse 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다. 이 연결된 서비스에 대한 자세한 내용은 [Azure SQL Data Warehouse 커넥터](data-factory-azure-sql-data-warehouse-connector.md#linked-service-properties) 문서를 참조하세요.

## <a name="sql-server-linked-service"></a>SQL Server 연결된 서비스
SQL Server 연결된 서비스를 만들고 [저장 프로시저 활동](data-factory-stored-proc-activity.md) 에서 사용하여 Data Factory 파이프라인에서 저장 프로시저를 호출합니다. 이 연결된 서비스에 대한 자세한 내용은 [SQL Server 커넥터](data-factory-sqlserver-connector.md#linked-service-properties) 문서를 참조하세요.

