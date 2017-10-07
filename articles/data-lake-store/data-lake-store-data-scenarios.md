---
title: "데이터 레이크 저장소를 포함 하는 aaaData 시나리오 | Microsoft Docs"
description: "수집 된 처리, 다운로드 하 여 데이터 레이크 저장소에서 시각화 hello 다양 한 시나리오 및 데이터를 사용 하 여 도구 수를 이해합니다"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 37409a71-a563-4bb7-bc46-2cbd426a2ece
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: caaa3979b8a2532089778c3e3db3c711714d3c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-data-lake-store-for-big-data-requirements"></a>빅 데이터 요구 사항에 Azure Data Lake 저장소 사용
빅 데이터 처리에는 네 가지 주요 단계가 있습니다.

* 실시간으로 또는 배치로 대량의 데이터를 데이터 저장소에 수집
* Hello 데이터 처리
* Hello 데이터 다운로드
* Hello 데이터 시각화

이 문서에서는 의견에 귀 이러한 단계에서 존중 tooAzure 데이터 레이크 저장소 toounderstand hello 옵션 및 도구 사용 가능한 toomeet와 빅 데이터 요구 사항입니다.

## <a name="ingest-data-into-data-lake-store"></a>Data Lake 저장소에 데이터 수집
이 섹션에는 hello 다양 한 원본 데이터와 hello 다양 한 방법으로 데이터 레이크 저장소 계정에 해당 데이터를 ingested 수 있는 강조 표시 합니다.

![Data Lake Store에 데이터 수집](./media/data-lake-store-data-scenarios/ingest-data.png "Data Lake Store에 데이터 수집")

### <a name="ad-hoc-data"></a>임시 데이터
빅 데이터 응용 프로그램의 프로토타입 제작에 사용되는 작은 데이터 집합을 나타냅니다. 여러 가지 방법으로 hello hello 데이터 원본에 따라 임시 데이터를 수집 하는 방법의 수입니다.

| 데이터 원본 | 로컬 컴퓨터를 사용하여 |
| --- | --- |
| 수집 |<ul> <li>[Azure Portal](/data-lake-store-get-started-portal.md)</li> <li>[Azure PowerShell](data-lake-store-get-started-powershell.md)</li> <li>[Azure 플랫폼 간 CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li> <li>[Visual Studio용 Data Lake 도구를 사용하여 U-SQL 스크립트 만들기](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md) </li></ul> |
| Azure 저장소 Blob |<ul> <li>[Azure 데이터 팩터리](../data-factory/data-factory-azure-datalake-connector.md)</li> <li>[AdlCopy 도구](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[HDInsight 클러스터에서 실행되는 DistCp](data-lake-store-copy-data-wasb-distcp.md)</li> </ul> |

### <a name="streamed-data"></a>스트리밍된 데이터
응용 프로그램, 장치, 센서 등 다양한 원본을 통해 생성할 수 있는 데이터를 나타냅니다. 이 데이터는 다양한 도구를 사용하여 Data Lake 저장소에 수집할 수 있습니다. 이러한 도구는 일반적으로 캡처하고에서 이벤트에서 이벤트 별로 hello 데이터 처리 실시간으로 다음 hello 이벤트를에서 쓰는 일괄 처리 데이터 레이크 저장소에 추가로 처리 될 수 있도록 합니다.

다음은 사용할 수 있는 도구입니다.

* [Azure 스트림 분석](../stream-analytics/stream-analytics-data-lake-output.md) -이벤트 수집 된 이벤트 허브로 쓸 수 있습니다 tooAzure 데이터 레이크 출력은 Azure 데이터 레이크 저장소를 사용 하 여 합니다.
* [Azure HDInsight 스톰](../hdinsight/hdinsight-storm-write-data-lake-store.md) -tooData Lake 저장소에서 Storm 클러스터 hello 직접 데이터를 쓸 수 있습니다.
* [EventProcessorHost](../event-hubs/event-hubs-dotnet-standard-getstarted-receive-eph.md) – 이벤트 허브에서 이벤트를 수신 하 고 다음 써야 tooData Lake 저장소 hello를 사용 하 여 [데이터 레이크 저장소.NET SDK](data-lake-store-get-started-net-sdk.md)합니다.

### <a name="relational-data"></a>관계형 데이터
관계형 데이터베이스의 데이터를 원본으로 사용할 수도 있습니다. 관계형 데이터베이스는 일정 기간 동안 엄청난 양의 데이터를 수집합니다. 이 데이터를 빅 데이터 파이프라인을 통해 처리하면 중요한 정보를 얻을 수 있습니다. 데이터 레이크 저장소로 hello 도구 toomove 다음 이러한 데이터를 사용할 수 있습니다.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure 데이터 팩터리](../data-factory/data-factory-data-movement-activities.md)

### <a name="web-server-log-data-upload-using-custom-applications"></a>웹 서버 로그 데이터(사용자 지정 응용 프로그램을 사용하여 업로드)
웹 서버 로그 데이터의 분석 빅 데이터 응용 프로그램에 대 한 일반적인 사용 사례 이며 많은 양의 파일 toobe 로그 업로드 toohello 데이터 레이크 저장소가 필요 하기 때문에이 유형의 데이터 집합 특별히 호출 됩니다. Hello 도구 toowrite 뒤의 모든 사용자 고유의 스크립트 또는 응용 프로그램 tooupload를 사용할 수 있습니다 이러한 데이터입니다.

* [Azure 플랫폼 간 CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake 저장소 .NET SDK](data-lake-store-get-started-net-sdk.md)
* [Azure 데이터 팩터리](../data-factory/data-factory-data-movement-activities.md)

웹 서버 로그 데이터를 업로드 하기 위한 또한 다른 종류의 데이터 (예: 소셜 표현의 데이터)를 업로드 하기 위한 것이 좋은 접근 toowrite 사용자 고유의 사용자 지정 스크립트/응용 프로그램 수 있기 때문에 hello 유연성 tooinclude 데이터 일부로 구성 요소를 업로드 하는 중 더 큰 빅 데이터 응용 프로그램입니다. 일부 경우에이 코드는 스크립트 또는 간단한 명령줄 유틸리티의 hello 양식을 걸릴 수 있습니다. 경우에 따라 hello 코드 비즈니스 응용 프로그램이 나 솔루션에 사용 되는 toointegrate 빅 데이터 처리를 수 있습니다.

### <a name="data-associated-with-azure-hdinsight-clusters"></a>Azure HDInsight 클러스터와 연결된 데이터
대부분의 HDInsight 클러스터 유형(Hadoop, HBase, Storm)은 데이터 저장소 리포지토리로 Data Lake 저장소를 지원합니다. HDInsight 클러스터는 Azure 저장소 Blob(WASB)에서 데이터에 액세스합니다. 성능 향상을 위해 hello 클러스터와 연결 된 데이터 레이크 저장소 계정으로 WASB에서 hello 데이터를 복사할 수 있습니다. 다음 도구 toocopy hello 데이터 hello를 사용할 수 있습니다.

* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)
* [AdlCopy Service](data-lake-store-copy-data-azure-storage-blob.md)
* [Azure 데이터 팩터리](../data-factory/data-factory-azure-datalake-connector.md)

### <a name="data-stored-in-on-premises-or-iaas-hadoop-clusters"></a>온-프레미스 또는 IaaS Hadoop 클러스터에 저장된 데이터
HDFS를 사용하여 로컬 컴퓨터의 기존 Hadoop 클러스터에 대량의 데이터를 저장할 수 있습니다. hello Hadoop 클러스터는 온-프레미스 배포에 있을 수 있습니다 또는 Azure에서는 IaaS 클러스터 내에서 수 있습니다. 이러한 데이터 tooAzure Data Lake 저장소에 적절 하 게 되풀이 또는 일회용 접근 방식에 대 한 요구 사항 toocopy 수 있습니다. 사용할 수 있는 tooachieve이 다양 한 옵션이 있습니다. 다음은 대체 목록 및 hello 장점과 단점을 이해 합니다.

| 접근 방식 | 세부 정보 | 장점 | 고려 사항 |
| --- | --- | --- | --- |
| Azure 데이터 팩터리 (ADF) toocopy 데이터를 사용 하 여 Hadoop 클러스터 tooAzure 데이터 레이크 저장소에서 직접 |[ADF는 데이터 원본으로 HDFS 지원](../data-factory/data-factory-hdfs-connector.md) |ADF는 HDFS에 대한 기본 지원과 일등급 종단 간 관리 및 모니터링을 제공합니다. |사용 하려면 데이터 관리 게이트웨이 toobe 온-프레미스를 배포 또는 hello IaaS 클러스터 |
| Hadoop에서 데이터를 파일로 내보냅니다. 그런 다음 적절 한 메커니즘을 사용 하 여 hello 파일 tooAzure 데이터 레이크 저장소를 복사 합니다. |사용 하 여 파일 tooAzure Data Lake 저장소에 복사할 수 있습니다. <ul><li>[Windows OS용 Azure PowerShell](data-lake-store-get-started-powershell.md)</li><li>[비Windows OS용 Azure 플랫폼 간 CLI 2.0](data-lake-store-get-started-cli-2.0.md)</li><li>Data Lake Store SDK를 사용하는 사용자 지정 앱</li></ul> |빠른 tooget 시작 되었습니다. 맞춤 업로드를 수행할 수 있습니다. |여러 기술을 사용하는 다단계 절차입니다. 관리 및 모니터링 증가 하는 것이 어려울 toobe hello 도구의 지정 된 시간이 hello 사용자 지정 특성 |
| Distcp toocopy 데이터 Hadoop tooAzure 저장소를에서 사용 합니다. 그런 다음 적절 한 메커니즘을 사용 하 여 Azure 저장소 tooData Lake 저장소에서 데이터를 복사 합니다. |사용 하 여 Azure 저장소 tooData Lake 저장소에서 데이터를 복사할 수 있습니다. <ul><li>[Azure 데이터 팩터리](../data-factory/data-factory-data-movement-activities.md)</li><li>[AdlCopy 도구](data-lake-store-copy-data-azure-storage-blob.md)</li><li>[HDInsight 클러스터에서 실행되는 Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)</li></ul> |오픈 소스 도구를 사용할 수 있습니다. |여러 기술을 사용하는 다단계 절차입니다. |

### <a name="really-large-datasets"></a>매우 큰 데이터 집합
범위 테라바이트까지에 있는 데이터 집합을 업로드 하는 것에 대 한 위의 hello 방법을 사용 하 여 수 있습니다 느리고 비용이 많이 드는. 이 경우 아래 hello 옵션을 사용할 수 있습니다.

* **Azure Express 경로 사용**. Azure Express 경로를 사용하면 온-프레미스의 인프라와 Azure 데이터 센터 사이에 개인 연결을 만들 수 있습니다. 이렇게 하면 대용량 데이터를 안전하게 전송할 수 있습니다. 자세한 내용은 [Azure Express 경로 설명서](../expressroute/expressroute-introduction.md)를 참조하세요.
* **데이터를 "오프라인"으로 업로드**. Azure ExpressRoute를 사용 하 여 적절 하지 않은 어떤 이유로 든 사용할 수 있습니다 [Azure 가져오기/내보내기 서비스](../storage/common/storage-import-export-service.md) 데이터 tooan Azure 데이터 센터에 있는 tooship 하드 디스크 드라이브입니다. 데이터가 첫 번째 업로드 tooAzure 저장소 Blob 됩니다. 사용할 수 있습니다 [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) 또는 [AdlCopy 도구](data-lake-store-copy-data-azure-storage-blob.md) toocopy 데이터를 Azure 저장소 Blob tooData Lake 저장소입니다.

  > [!NOTE]
  > 가져오기/내보내기 서비스를 hello를 사용 하 여, 동안 hello 디스크 배송 tooAzure 데이터 센터에서 hello 파일 크기 195 g B 보다 크지 않아야 합니다.
  >
  >

## <a name="process-data-stored-in-data-lake-store"></a>Data Lake 저장소에 저장된 데이터 처리
데이터 레이크 저장소의 hello 데이터를 사용할 수 있는 hello를 사용 하 여 데이터 빅 데이터 응용 프로그램을 지원 하는지 분석에서 실행할 수 있습니다. 현재 데이터 레이크 저장소에 저장 된 hello 데이터에서 Azure HDInsight 및 Azure 데이터 레이크 분석 toorun 데이터 분석 작업을 사용할 수 있습니다.

![Data Lake Store의 데이터 분석](./media/data-lake-store-data-scenarios/analyze-data.png "Data Lake Store의 데이터 분석")

다음 예제는 hello 볼 수 있습니다.

* [Data Lake 저장소를 저장소로 사용하여 HDInsight 클러스터 만들기](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용](../data-lake-analytics/data-lake-analytics-get-started-portal.md)

## <a name="download-data-from-data-lake-store"></a>Data Lake 저장소에서 데이터 다운로드
또한 toodownload 원하는 또는에서 데이터를 이동할 Azure 데이터 레이크 저장소 시나리오와 같은 수 있습니다.

* 기존 데이터 처리 파이프라인으로 tooother 저장소 toointerface 데이터를 이동 합니다. 예를 들어 있습니다 데이터 레이크 저장소 tooAzure SQL 데이터베이스에서에서 데이터 toomove 하거나 온-프레미스 SQL Server.
* IDE 환경에서 응용 프로그램 프로토타입을 빌드하는 동안 처리를 위해 데이터 tooyour 로컬 컴퓨터를 다운로드 합니다.

![Data Lake Store에서 데이터 송신](./media/data-lake-store-data-scenarios/egress-data.png "Data Lake Store에서 데이터 송신")

이러한 경우 hello 다음 옵션 중 하나를 사용할 수 있습니다.

* [Apache Sqoop](data-lake-store-data-transfer-sql-sqoop.md)
* [Azure 데이터 팩터리](../data-factory/data-factory-data-movement-activities.md)
* [Apache DistCp](data-lake-store-copy-data-wasb-distcp.md)

작업을 데이터 레이크 저장소에서 직접 스크립트/응용 프로그램 toodownload 데이터 hello toowrite 메서드 다음으로 사용할 수도 합니다.

* [Azure 플랫폼 간 CLI 2.0](data-lake-store-get-started-cli-2.0.md)
* [Azure PowerShell](data-lake-store-get-started-powershell.md)
* [Azure Data Lake 저장소 .NET SDK](data-lake-store-get-started-net-sdk.md)

## <a name="visualize-data-in-data-lake-store"></a>Data Lake 저장소에서 데이터 시각화
데이터 레이크 저장소에 저장 된 데이터 서비스 toocreate 시각적 표시를 혼합 하 여 사용할 수 있습니다.

![Data Lake Store에서 데이터 시각화](./media/data-lake-store-data-scenarios/visualize-data.png "Data Lake Store에서 데이터 시각화")

* 사용 하 여 시작할 수 있습니다 [Azure Data Factory toomove 데이터로 데이터 레이크 저장소 tooAzure SQL 데이터 웨어하우스](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)
* 그 후 수 [Azure SQL 데이터 웨어하우스와 Power BI 통합](../sql-data-warehouse/sql-data-warehouse-integrate-power-bi.md) toocreate hello 데이터의 시각적 표현입니다.
