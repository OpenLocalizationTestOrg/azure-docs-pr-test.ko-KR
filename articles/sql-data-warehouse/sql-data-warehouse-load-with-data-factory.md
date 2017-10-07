---
title: "aaaLoad 데이터를 Azure SQL 데이터 웨어하우스에 – Data Factory | Microsoft Docs"
description: "이 자습서에서는 Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스로 데이터를 로드 하 고 hello 데이터 원본으로 SQL Server 데이터베이스를 사용 합니다."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse;azure-data-factory
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: loading
ms.date: 02/08/2017
ms.author: cakarst;barbkess
ms.openlocfilehash: 471871d3ee00ab34cc84bb63fbd13a323d14c2b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-sql-data-warehouse-with-data-factory"></a>Data Factory와 함께 SQL Data Warehouse로 데이터 로드

Azure Data Factory tooload 데이터를 사용 하 여 hello 중 하나에서 Azure SQL 데이터 웨어하우스로 [원본 데이터 저장소를 지원](../data-factory/data-factory-data-movement-activities.md#supported-data-stores-and-formats)합니다. 예를 들어 Data Factory를 사용하여 Azure SQL Database 또는 Oracle 데이터베이스에서 SQL Data Warehouse로 데이터를 로드할 수 있습니다. 이 문서의 자습서 tooload 데이터는 온-프레미스 SQL Server에서 SQL 데이터 웨어하우스 데이터베이스 방법을 보여 줍니다.

**예상 시간**: hello 전제 조건이 충족 되 면이 자습서는 10-15 분 toocomplete에 대 한 합니다.

## <a name="prerequisites"></a>필수 조건

- 필요한는 **SQL Server 데이터베이스** hello 데이터가 포함 된 테이블이 있는 toobe 복사한 toohello SQL 데이터 웨어하우스 합니다.  

- 온라인 **SQL Data Warehouse**가 필요합니다. 데이터 웨어하우스 아직 없는 경우 너무 방법을 알아볼[Azure SQL 데이터 웨어하우스를 만들](sql-data-warehouse-get-started-provision.md)합니다.

- **Azure Storage 계정**이 필요합니다. 저장소 계정이 아직 없는 경우 너무 방법을 알아볼[저장소 계정 만들기](../storage/common/storage-create-storage-account.md)합니다. 최상의 성능을 위해 hello 저장소 계정을 찾는 및 hello에 hello 데이터 웨어하우스 동일한 Azure 지역입니다.

## <a name="configure-a-data-factory"></a>Data Factory 구성
1. Toohello 로그인 [Azure 포털][]합니다.
2. 데이터 웨어하우스를 찾아 클릭 tooopen 것입니다.
3. Hello 주 블레이드에서 클릭 **데이터 로드** > **Azure Data Factory**합니다.

    ![데이터 로드 마법사 시작](media/sql-data-warehouse-load-with-data-factory/launch-load-data-wizard.png)

4. Azure 구독에는 데이터 팩터리 없는 경우 표시는 **새 데이터 팩터리** hello 브라우저의 별도 탭에서 대화 상자. Hello에 요청 된 정보를 누르고 **만들기**합니다. Hello 데이터 팩터리를 만든 후 hello **새 데이터 팩터리** 대화 상자가 닫히고 hello 참조 **데이터 팩터리 선택** 대화 상자.

    Hello 참조 hello Azure 구독에 이미 하나 이상의 데이터 팩터리를 사용 하도록 설정한 경우 **데이터 팩터리 선택** 대화 상자. 이 대화 상자에서 기존 데이터 팩토리를 선택 하거나 클릭 **새 데이터 팩터리 만들기** toocreate 새 합니다.

    ![데이터 팩터리 구성](media/sql-data-warehouse-load-with-data-factory/configure-data-factory.png)

5. Hello에 **데이터 팩터리 선택** 대화 상자, hello **데이터 로드** 옵션은 기본적으로 선택 합니다. 클릭 **다음** toostart 태스크를 로드 하는 데이터를 만듭니다.

## <a name="configure-hello-data-factory-properties"></a>Hello 데이터 팩터리의 속성 구성
데이터 팩터리를 만들었으므로 이제 hello 다음 단계는 tooconfigure hello 데이터 로드 작업 일정입니다.

1. **작업 이름**에 **DWLoadData-fromSQLServer**를 입력합니다.
2. Hello 기본값을 사용 하 여 **이제 한 번 실행** 옵션을 클릭 하 여 **다음**합니다.

    ![로드 일정 구성](media/sql-data-warehouse-load-with-data-factory/configure-load-schedule.png)

## <a name="configure-hello-source-data-store-and-gateway"></a>Hello 원본 데이터 저장소 및 게이트웨이 구성
이제 Data Factory tooload 데이터 원하는 hello 온-프레미스 SQL Server 데이터베이스에 대 한 지시할 수 있습니다.

1. 선택 **SQL Server** 지원 hello 원본 데이터에서 카탈로그를 저장 하 고 클릭 **다음**합니다.

    ![SQL Server 원본 선택](media/sql-data-warehouse-load-with-data-factory/choose-sql-server-source.png)

2. A **지정 hello 온-프레미스 SQL Server 데이터베이스** 대화 상자가 나타납니다. 먼저 hello **연결 이름** 필드는 자동으로 채워집니다. hello 두 번째 필드의 hello hello 이름에 대 한 요청 **게이트웨이**합니다. 게이트웨이 이미가지고 있는 기존 데이터 팩토리를 사용 하는 hello 드롭 다운 목록에서 선택 하 여 hello 게이트웨이 다시 사용할 수 있습니다. Hello 클릭 **게이트웨이 만들기** toocreate 데이터 관리 게이트웨이 연결 합니다.  

    > [!NOTE]
    > Hello 원본 데이터를 저장 하는 경우 온-프레미스 이거나 Azure IaaS 가상 컴퓨터에서 데이터 관리 게이트웨이가 필요 합니다. 게이트웨이는 Data Factory와 1-1 관계를 갖습니다. 다른 data factory에서 사용할 수 없지만 hello에 있는 작업을 로드 하는 여러 데이터에서 사용할 수 같은 데이터 팩터리입니다. 게이트웨이는 데이터 로드 작업을 실행할 때 사용 되는 tooconnect toomultiple 데이터 저장소를 수 있습니다.
    >
    > Hello 게이트웨이에 대 한 자세한 내용은 참조 [데이터 관리 게이트웨이](../data-factory/data-factory-data-management-gateway.md) 문서.

3. **게이트웨이 만들기** 대화 상자가 나타납니다. 이름에는 **GatewayForDWLoading**을 입력하고 **만들기**를 클릭합니다.

4. **게이트웨이 구성** 대화 상자가 나타납니다. 클릭 **이 컴퓨터에 빠른 설치를 시작** tooautomatically 다운로드, 설치 및 현재 시스템에 데이터 관리 게이트웨이 등록 합니다. hello 진행률 팝업 창에 표시 됩니다. Hello 컴퓨터 toohello 데이터 저장소에 연결할 수 없는 경우 수동으로 실행할 수 있습니다 [hello 게이트웨이 다운로드 및 설치](https://www.microsoft.com/download/details.aspx?id=39717) toohello 데이터를 연결할 수 있는 컴퓨터에 저장 하 고 다음 키 tooregister hello를 사용 합니다.
    > [!NOTE]
    > 빠른 설치 hello Microsoft Edge 및 Internet Explorer에서 고유 하 게 작동합니다. Google Chrome을 사용 하는 경우 먼저 크롬 웹 저장소에서 hello ClickOnce 확장을 설치 합니다.

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/launch-express-setup.png)

5. Hello 게이트웨이 설치 toocomplete 될 때까지 기다립니다. Hello 게이트웨이 등록 하 고 온라인 상태를 hello 팝업 창이 닫히고 hello 새 게이트웨이 hello 게이트웨이 필드에 나타납니다. 다음 채우기 hello rest에서 필수 필드 다음과 같이, 클릭 **다음**합니다.
    - **서버 이름**: hello의 이름 온-프레미스 SQL Server.
    - **데이터베이스 이름**: SQL Server 데이터베이스.
    - **자격 증명 암호화**: 웹 브라우저"에서" hello 기본값을 사용 합니다.
    - **인증 유형**: hello 사용 중인 인증 유형을 선택 합니다.
    - **사용자 이름** 및 **암호**: 권한 toocopy hello 데이터를 가진 사용자에 대 한 hello 사용자 이름 및 암호를 입력 합니다.

    ![빠른 설치 시작](media/sql-data-warehouse-load-with-data-factory/configure-sql-server.png)

6. hello 다음 단계는 toocopy hello 데이터에서 toochoose hello 테이블입니다. 키워드를 사용 하 여 hello 테이블을 필터링 할 수 있습니다. 및 hello 아래쪽 패널에서 hello 데이터와 테이블 스키마를 미리 볼 수 있습니다. 선택을 완료했으면 **다음**을 클릭합니다.

    ![테이블 선택](media/sql-data-warehouse-load-with-data-factory/select-tables.png)

## <a name="configure-hello-destination-your-sql-data-warehouse"></a>Hello 대상, SQL 데이터 웨어하우스 구성

이제 Data Factory hello 대상 정보에 대 한 지시할 수 있습니다.

1. SQL Data Warehouse 연결 정보가 자동으로 채워집니다. Hello 사용자 이름에 대 한 hello 암호를 입력 합니다. **다음**을 클릭합니다.

    ![대상 구성](media/sql-data-warehouse-load-with-data-factory/configure-destination.png)

2. 지능형 테이블 매핑 테이블 이름에 따라 소스 toodestination 테이블을 매핑하는 나타납니다. Hello 테이블이 hello 대상에 존재 하지 않는 경우 기본적으로 ADF 만들어집니다 hello로 동일한 이름 (이 적용 tooSQL 서버 또는 원본으로 Azure SQL 데이터베이스). 또한 toomap tooan 기존 테이블을 선택할 수 있습니다. 검토하고 **다음**을 클릭합니다.

    ![맵 테이블](media/sql-data-warehouse-load-with-data-factory/table-mapping.png)

3. Hello 스키마 매핑을 검토 하 고 오류 또는 경고 메시지를 찾아보십시오. 지능형 매핑은 열 이름을 기반으로 합니다. Hello 원본 및 대상 열 간에 변환 하는 지원 되지 않는 데이터 형식 변환을 이면 hello 해당 테이블과 함께 오류 메시지가 표시 됩니다. Toolet Data Factory 자동을 선택 하면 hello 테이블 만들기, 적절 한 데이터 형식 변환이 필요한 소스 및 대상 저장소 간 toofix hello 호환 되지 않는 경우 발생할 수 있습니다.

    ![맵 스키마](media/sql-data-warehouse-load-with-data-factory/schema-mapping.png)

4. **다음**을 누릅니다.

## <a name="configure-hello-performance-settings"></a>Hello 성능 설정 구성
Azure 저장소 계정을 사용 하 여 SQL 데이터 웨어하우스 효율적으로 로드 하기 전에 hello 데이터 준비에 사용 되는 hello 성능 구성에서 구성한 [PolyBase](sql-data-warehouse-best-practices.md#use-polybase-to-load-and-export-data-quickly)합니다. Hello 복사를 완료 한 후 hello 중간 데이터 저장소에는 자동으로 정리 합니다.

기존 Azure Storage 계정을 선택하거나 **다음**을 클릭합니다.

![준비 Blob 구성](media/sql-data-warehouse-load-with-data-factory/configure-staging-blob.png)

## <a name="review-summary-information-and-deploy-hello-pipeline"></a>요약 정보를 검토 하 고 hello 파이프라인 배포

Hello 구성을 검토 하 고 클릭 **마침** 단추 toodeploy hello 파이프라인.

![데이터 팩터리 배포](media/sql-data-warehouse-load-with-data-factory/deploy-data-factory.png)

## <a name="monitor-data-loading-progress"></a>데이터 로드 진행 상태 모니터

Hello 배포 진행률과 hello에 결과 볼 수 있습니다 **배포** 페이지.

1. Hello 배포 작업이 완료 되 면 hello 링크는 클릭 **toomonitor 복사 파이프라인 여기를 클릭** toomonitor 데이터 진행 상태를 로드 합니다.

    ![파이프라인 모니터링](media/sql-data-warehouse-load-with-data-factory/monitor-pipeline.png)

2. 새로 만든 hello **DWLoadData fromSQLServer** 데이터 로드 파이프라인은 자동으로 hello 왼쪽에서 선택 **리소스 탐색기**합니다.

    ![파이프라인 보기](media/sql-data-warehouse-load-with-data-factory/view-pipeline.png)

3. Hello 가운데에 hello 파이프라인에는 클릭 패널 toosee hello tooan 활동을 매핑하는 각 테이블에 대 한 상태를 자세히 설명 합니다.

    ![테이블 활동 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity.png)

4. 작업 내부로 누르고 데이터 크기, 행, 처리량 등을 포함 하 여 hello 오른쪽 패널에서 세부 정보를 로드 하는 hello 데이터 참조 추가 합니다.

    ![테이블 활동 세부 정보 보기](media/sql-data-warehouse-load-with-data-factory/view-table-activity-details.png)

5. toolaunch이 모니터링 보기 이상, 이동 tooyour SQL 데이터 웨어하우스, 클릭 **데이터 로드 > Azure Data Factory**공장을 선택 하 고 선택 **작업 로드를 기존 모니터링**합니다.

## <a name="next-steps"></a>다음 단계

toomigrate 프로그램 데이터베이스 tooSQL 데이터 웨어하우스 참조 [마이그레이션 개요](sql-data-warehouse-overview-migrate.md)합니다.

Azure Data Factory와 해당 데이터 이동 기능에 대해 자세히 toolearn hello 다음 문서 참조:

- [소개 tooAzure 데이터 팩터리](../data-factory/data-factory-introduction.md)
- [복사 작업을 사용하여 데이터 이동](../data-factory/data-factory-data-movement-activities.md)
- [Azure 데이터 팩터리를 사용 하 여 Azure SQL 데이터 웨어하우스 로부터 데이터 tooand 이동](../data-factory/data-factory-azure-sql-data-warehouse-connector.md)

tooexplore SQL 데이터 웨어하우스에 데이터 참조 문서 다음 hello:

- [Visual Studio와 SSDT를 사용 하 여 데이터 웨어하우스 tooSQL 연결](sql-data-warehouse-query-visual-studio.md)
- [Power BI를 사용하여 시각적 데이터](sql-data-warehouse-get-started-visualize-with-power-bi.md)

<!-- Azure references -->
[Azure 포털]: https://portal.azure.com
