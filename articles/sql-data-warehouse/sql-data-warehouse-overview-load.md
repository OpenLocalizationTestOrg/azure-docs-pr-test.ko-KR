---
title: "aaaLoad 데이터를 Azure SQL 데이터 웨어하우스에 | Microsoft Docs"
description: "SQL 데이터 웨어하우스를 로드 하는 데이터에 대 한 hello 일반적인 시나리오에 알아봅니다. 여기에는 PolyBase, Azure Blob 저장소, 플랫 파일 및 디스크 배송 사용이 포함됩니다. 타사 도구를 사용할 수도 있습니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a>Azure SQL 데이터 웨어하우스에 데이터 로드
Hello 시나리오 옵션 및 SQL 데이터 웨어하우스로 데이터를 로드 하기 위한 권장 사항을 요약 합니다.

hello 부하에 대 한 데이터를 로드 하의 가장 어려운 일부 hello hello 데이터 준비 중 일반적으로입니다. Azure 데이터 팩터리를 사용 하 여 사이의 통신 및 데이터 이동 tooorchestrate hello Azure 서비스를 azure hello 서비스의 대부분에 대 한 일반 데이터 저장소로 Azure blob 저장소를 사용 하 여 로드 간단 합니다. 이러한 프로세스는 Azure blob 저장소에서 동시에 (MPP) tooload 데이터를 SQL 데이터 웨어하우스에 방대한 병렬 처리를 사용 하 여 PolyBase 기술을와 통합 됩니다. 

샘플 데이터베이스를 로드하는 자습서의 경우 [샘플 데이터베이스 로드][Load sample databases]를 참조하세요.

## <a name="load-from-azure-blob-storage"></a>Azure Blob 저장소에서 로드
SQL 데이터 웨어하우스로 hello 가장 빠른 방법은 tooimport 데이터 toouse PolyBase tooload 데이터 Azure blob 저장소의 경우 PolyBase 사용 하 여 SQL 데이터 웨어하우스의는 방대한 병렬 Azure blob 저장소에서 동시에 (MPP) 디자인 tooload 데이터를 처리 합니다. PolyBase toouse T-SQL 명령이 나 Azure 데이터 팩터리 파이프라인을 사용할 수 있습니다.

### <a name="1-use-polybase-and-t-sql"></a>1. PolyBase 및 T-SQL 사용
로드 프로세스 요약:

1. 데이터 tooAzure blob 저장소 또는 Azure 데이터 레이크 저장소를 이동 하 고 텍스트 파일에 저장 합니다.
2. SQL 데이터 웨어하우스 toodefine hello 위치와 hello 데이터의 형식에 외부 개체를 구성
3. 새 데이터베이스 테이블에 병렬로 T-SQL 명령 tooload hello 데이터를 실행 합니다.

<!-- 5. Schedule and run a loading job. --> 

자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.

### <a name="2-use-azure-data-factory"></a>2. Azure Data Factory 사용
더 간단한 방법은 toouse PolyBase, SQL 데이터 웨어하우스로 PolyBase tooload 데이터 Azure blob 저장소를 사용 하는 Azure 데이터 팩터리 파이프라인을 만들 수 있습니다. Toodefine hello T-SQL 개체 필요 하지 않으므로 빠른 tooconfigure입니다. Tooquery hello 외부 데이터를 가져오지 않고 해야 할 경우 T-SQL을 사용 합니다. 

로드 프로세스 요약:

1. 사용자가 데이터 tooAzure blob 저장소를 이동 하 고 텍스트 파일에 저장 합니다. Azure Data Factory는 현재 PolyBase와의 ADLS 연결을 지원하지 않습니다.
2. Azure 데이터 팩터리 파이프라인 tooingest hello 데이터를 만듭니다. Hello PolyBase 옵션을 사용 합니다.
4. 예약 하 고 hello 파이프라인을 실행 합니다.

자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (Azure 데이터 팩터리)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]합니다.

## <a name="load-from-sql-server"></a>SQL Server에서 로드
tooload 데이터 tooSQL SQL Server Integration Services (SSIS)를 사용할 수는 데이터 웨어하우스를에서 플랫 파일을 전송 하거나 디스크 tooMicrosoft를 제공 합니다. 다른 프로세스와 링크 tootutorials 로드 hello에 대 한 요약 toosee 계속 읽어 보십시오.

데이터 웨어하우스 SQL Server tooSQL에서 전체 데이터 마이그레이션을 tooplan 참조 hello [마이그레이션 개요][Migration overview]합니다. 

### <a name="use-integration-services-ssis"></a>Integration Services(SSIS) 사용
SQL Server에 Integration Services (SSIS) 패키지 tooload을 이미 사용 중인 경우에 hello 소스 및 hello 대상으로 SQL 데이터 웨어하우스 사용자 패키지 toouse SQL Server를 업데이트할 수 있습니다. 이 신속 하 게 하 고 쉽게 toodo 시도 하지 않는 toomigrate 사용자 로드에 적합 한 선택 인지 hello 클라우드에서 이미 toouse 데이터를 처리 합니다. hello 단점은 hello 부하 PolyBase를 사용 하 여이 SSIS 병렬로 hello 부하를 수행 하지 않으므로 보다 느리다는 것입니다.

로드 프로세스 요약:

1. Hello 원본에 대 한 Integration Services 패키지 toopoint toohello SQL Server 인스턴스 및 hello 대상에 대 한 hello SQL 데이터 웨어하우스 데이터베이스를 수정 합니다.
2. 없는 아직 없는 경우 프로그램 스키마 tooSQL 데이터 웨어하우스를 마이그레이션하십시오.
3. SQL 데이터 웨어하우스에서 지 원하는 hello 데이터 형식만 사용 하는 경우 패키지에 hello 매핑을 변경 합니다.
4. 예약 하 고 hello 패키지를 실행 합니다.

자습서를 참조 하십시오. [SQL Server tooAzure SQL 데이터 웨어하우스 (SSIS)에서 데이터를 로드할][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]합니다.

### <a name="use-azcopy-recommended-for--10-tb-data"></a>AZCopy 사용(10TB 미만의 데이터에 권장)
데이터 크기 < 10TB 인 경우 SQL Server tooflat 파일에서 hello 데이터를 내보낼, hello 파일 tooAzure blob 저장소에 복사한 다음 PolyBase tooload hello 데이터를 사용 하 여 SQL 데이터 웨어하우스로

로드 프로세스 요약:

1. SQL Server tooflat 파일에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.
2. Hello AZCopy 명령줄 유틸리티 toocopy 플랫 파일 tooAzure blob 저장소에서 데이터를 사용 합니다.
3. SQL 데이터 웨어하우스로 tooload PolyBase를 사용 합니다.

자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.

### <a name="use-bcp"></a>bcp 사용
적은 양의 데이터가 있는 경우 bcp tooload Azure SQL 데이터 웨어하우스에 직접 사용할 수 있습니다.

로드 프로세스 요약:

1. SQL Server tooflat 파일에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.
2. Bcp tooload 데이터 범위를 플랫 파일을 tooSQL 데이터 웨어하우스에 직접 합니다.

자습서를 참조 하십시오. [SQL Server tooAzure SQL 데이터 웨어하우스 (bcp)에서 데이터를 로드할][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]합니다.

### <a name="use-importexport-recommended-for--10-tb-data"></a>가져오기/내보내기 사용(10TB를 초과하는 데이터에 권장)
데이터 크기가 > 10TB toomove를 원하는 경우 해당 tooAzure, 권장 서비스를 전달 합니다.이 디스크를 사용 하는 [가져오기/내보내기][Import/Export]합니다. 

로드 프로세스 요약

1. SQL Server tooflat 파일을 전송한 디스크에서 hello bcp 명령줄 유틸리티 tooexport 데이터를 사용 합니다.
2. Hello 디스크 tooMicrosoft 제공 됩니다.
3. Microsoft은 SQL 데이터 웨어하우스 hello 데이터 로드

## <a name="load-from-hdinsight"></a>HDInsight에서 로드
SQL 데이터 웨어하우스는 PolyBase 통해 HDInsight에서 데이터 로드를 지원합니다. hello 프로세스-PolyBase tooconnect tooHDInsight tooload 데이터를 사용 하 여 Azure Blob 저장소에서 데이터를 로드 동일 hello 됩니다. 

### <a name="1-use-polybase-and-t-sql"></a>1. PolyBase 및 T-SQL 사용
로드 프로세스 요약:

1. 데이터 tooHDInsight 이동 하 고 텍스트 파일에 저장 ORC, Parquet 형식입니다.
2. SQL 데이터 웨어하우스 toodefine hello 위치 및 hello 데이터 형식의 외부 개체를 구성 합니다.
3. 새 데이터베이스 테이블에 병렬로 T-SQL 명령 tooload hello 데이터를 실행 합니다.

자습서를 참조 하십시오. [Azure blob 저장소 tooSQL 데이터 웨어하우스 (PolyBase)에서 데이터를 로드할][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]합니다.

## <a name="recommendations"></a>권장 사항
상당수의 파트너에게는 로드 솔루션이 있습니다. 자세한 내용을 보려면 toofind 목록을 보려면 우리의 [솔루션 파트너][solution partners]합니다. 

데이터-관계형 원본에서 가져온 고로 SQL 데이터 웨어하우스 있습니다 tooload tootransform 필요 합니다 행과 열 로드 하기 전에 넣습니다. hello 변환 된 데이터는 데이터베이스에 저장 된 toobe 필요 하지 않습니다, 그리고 텍스트 파일에 저장할 수 있습니다.

새로 로드한 데이터에 대한 통계를 만듭니다. Azure SQL 데이터 웨어하우스는 자동 만들기 또는 통계 자동 업데이트를 아직 지원하지 않습니다.  순서 tooget hello 최상의 성능을 얻으려면 쿼리에서 것이 중요 toocreate 통계 hello 후 모든 테이블의 모든 열에 먼저 로드 또는 모든 변경이 hello 데이터에서 발생 합니다.  자세한 내용은 [통계][Statistics]를 참조하세요.

## <a name="next-steps"></a>다음 단계
더 많은 개발 팁에 대 한 참조 hello [개발 개요][development overview]합니다.

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
