---
title: "다른 Azure 서비스와 데이터 레이크 저장소 aaaIntegrating | Microsoft Docs"
description: "데이터 레이크 저장소가 다른 Azure 서비스와 통합하는 방법을 이해합니다."
documentationcenter: 
services: data-lake-store
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 48a5d1f4-3850-4c22-bbc4-6d1d394fba8a
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 839689f04623f8225884e7aa9c0b533a09323e80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="integrating-data-lake-store-with-other-azure-services"></a>데이터 레이크 저장소와 다른 Azure 서비스 통합
Azure 데이터 레이크 저장소 다른 Azure 서비스 tooenable 광범위 한 시나리오와 함께에서 사용할 수 있습니다. hello 다음 문서 hello는 서비스가 나열 데이터 레이크 저장소와 통합할 수 있습니다.

## <a name="use-data-lake-store-with-azure-hdinsight"></a>Azure HDInsight에 데이터 레이크 저장소 사용
프로 비전 할 수는 [Azure HDInsight](https://azure.microsoft.com/documentation/learning-paths/hdinsight-self-guided-hadoop-training/) 클러스터는 hello HDFS 호환 저장소로 데이터 레이크 저장소를 사용 합니다. 이 릴리스의 Windows 및 Linux의 Storm 및 Hadoop 클러스터의 경우 데이터 레이크 저장소를 추가 저장소로만 사용할 수 있습니다. 아직 이러한 클러스터가 hello 기본 저장소로 Azure 저장소 (WASB)를 사용합니다. 그러나 Windows 및 Linux에서 HBase 클러스터에 데이터 레이크 저장소 hello 기본 저장소 또는 추가 저장소 또는 둘 다로 사용할 수 있습니다.

데이터 레이크 저장소와 tooprovision HDInsight 클러스터 하는 방법에 지침은 다음을 참조 합니다.

* [Azure 포털을 사용하여 데이터 레이크 저장소로 HDInsight 클러스터 프로비전](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Azure PowerShell을 사용하여 Data Lake Store를 기본 저장소로 사용하는 HDInsight 클러스터 프로비전](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [Azure PowerShell을 사용하여 Data Lake Store를 추가 저장소로 사용하는 HDInsight 클러스터 프로비전](data-lake-store-hdinsight-hadoop-use-powershell.md)

## <a name="use-data-lake-store-with-azure-data-lake-analytics"></a>Azure 데이터 레이크 분석에 데이터 레이크 저장소 사용
[Azure Data Lake 분석](../data-lake-analytics/data-lake-analytics-overview.md) 클라우드 범위에서 toowork 빅 데이터와 함께 사용 하면 됩니다. 이를 통해 동적으로 리소스를 프로비전할 뿐만 아니라 지원되는 많은 데이터 원본(예: 데이터 레이크 저장소)에 저장될 수 있는 테라바이트 또는 심지어 엑사바이트의 데이터를 분석할 수 있습니다. Data Lake 분석은 최적화 된 특수 toowork와 Azure 데이터 레이크 저장소-hello 최고 수준의 성능, 처리량 및 병렬화를 빅 데이터 작업을 제공 합니다.

방법에 대 한 데이터 레이크 저장소와 Data Lake 분석 toouse 참조 [데이터 레이크 저장소를 사용 하 여 Data Lake 분석 시작](../data-lake-analytics/data-lake-analytics-get-started-portal.md)합니다.

## <a name="use-data-lake-store-with-azure-data-factory"></a>Azure Data Factory에 데이터 레이크 저장소 사용
사용할 수 있습니다 [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) tooingest 데이터를 Azure 테이블, Azure SQL 데이터베이스, Azure SQL 데이터 웨어하우스, Azure 저장소 Blob 및 온-프레미스 데이터베이스. Azure 데이터 팩터리는 hello Azure 에코 시스템에서에서 첫 번째 클래스 시민 되 고, 이러한 원본 tooAzure 데이터 레이크 저장소에서에서 데이터 사용된 tooorchestrate hello 수집 될 수 있습니다.

데이터 레이크 저장소와 Azure 데이터 팩터리 참조 하는 toouse 방법에 대 한 지침은 [데이터 팩터리를 사용 하 여 데이터 레이크 저장소에서 데이터 tooand 이동](../data-factory/data-factory-azure-datalake-connector.md)합니다.

## <a name="copy-data-from-azure-storage-blobs-into-data-lake-store"></a>Azure 저장소 Blob에서 데이터 레이크 저장소로 데이터 복사
Azure 데이터 레이크 저장소 AdlCopy toocopy 데이터가 Azure Blob 저장소에서 데이터 레이크 저장소 계정에 사용할 수 있게 하는 명령줄 도구를 제공 합니다. 자세한 내용은 참조 [Azure 저장소 Blob tooData Lake 저장소에서 데이터를 복사](data-lake-store-copy-data-azure-storage-blob.md)합니다.

## <a name="copy-data-between-azure-sql-database-and-data-lake-store"></a>Azure SQL 데이터베이스와 Data Lake 저장소 간에 데이터 복사
Apache Sqoop tooimport 사용을 Azure SQL 데이터베이스 및 데이터 레이크 저장소 간에 데이터를 내보낼 수 있습니다. 자세한 내용은 [Sqoop를 사용하여 Data Lake 저장소와 Azure SQL 데이터베이스 간에 데이터 복사](data-lake-store-data-transfer-sql-sqoop.md)를 참조하세요.

## <a name="use-data-lake-store-with-stream-analytics"></a>스트림 분석에 Data Lake 저장소 사용
데이터 레이크 저장소 hello 중 하나에서 Azure 스트림 분석을 사용 하 여 스트리밍 toostore 데이터를 출력으로 사용할 수 있습니다. 자세한 내용은 [Azure 스트림 분석을 사용하여 Azure 저장소 Blob에서 Data Lake 저장소에 데이터 스트리밍](data-lake-store-stream-analytics.md)을 참조하세요.

## <a name="use-data-lake-store-with-power-bi"></a>Power BI로 Data Lake 저장소 사용
데이터 레이크 저장소 계정 tooanalyze에서 Power BI tooimport 데이터를 사용할 수 있으며 hello 데이터 시각화. 자세한 내용은 [Power BI를 사용하여 Data Lake 저장소의 데이터 분석](data-lake-store-power-bi.md)을 참조하세요.

## <a name="use-data-lake-store-with-data-catalog"></a>Data Catalog로 Data Lake 저장소 사용
Azure Data Catalog toomake hello 데이터 hello 조직 전체에서 검색 가능한 hello에 데이터 레이크 저장소에서 데이터를 등록할 수 있습니다. 자세한 내용은 [Azure Data Catalog에 Data Lake 저장소의 데이터 등록](data-lake-store-with-data-catalog.md)을 참조하세요.

## <a name="use-data-lake-store-with-sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)에서 Data Lake Store 사용
Hello Azure 데이터 레이크 저장소 연결 관리자를 SSIS tooconnect Azure 데이터 레이크 저장소와 SSIS 패키지에서에서 사용할 수 있습니다. 자세한 내용은 [SSIS에서 Data Lake Store 사용](https://docs.microsoft.com/sql/integration-services/connection-manager/azure-data-lake-store-connection-manager)을 참조하세요.

## <a name="use-data-lake-store-with-sql-data-warehouse"></a>SQL Data Warehouse에서 Data Lake Store 사용
SQL 데이터 웨어하우스로 Azure 데이터 레이크 저장소에서 PolyBase tooload 데이터를 사용할 수 있습니다. 자세한 내용은 [SQL Data Warehouse에서 Data Lake Store 사용](../sql-data-warehouse/sql-data-warehouse-load-from-azure-data-lake-store.md)을 참조하세요.

## <a name="see-also"></a>참고 항목
* [Azure 데이터 레이크 저장소 개요](data-lake-store-overview.md)
* [포털을 사용하여 데이터 레이크 저장소 시작](data-lake-store-get-started-portal.md)
* [PowerShell을 사용하여 데이터 레이크 저장소 시작](data-lake-store-get-started-powershell.md)  

